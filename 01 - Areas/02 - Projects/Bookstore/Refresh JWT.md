## Step 3: RefreshTokenService

Implement service that handles:

- Token creation
    
- Verification of expiration
    
- Token deletion
    

Example:
```java
@Service
public class RefreshTokenService {

    @Value("${app.jwtRefreshExpirationMs}")
    private Long refreshTokenDurationMs;

    @Autowired
    private RefreshTokenRepository refreshTokenRepository;

    @Autowired
    private UserRepository userRepository;

    public RefreshToken createRefreshToken(Long userId) {
        RefreshToken refreshToken = new RefreshToken();
        refreshToken.setUser(userRepository.findById(userId).get());
        refreshToken.setExpiryDate(Instant.now().plusMillis(refreshTokenDurationMs));
        refreshToken.setToken(UUID.randomUUID().toString());
        refreshToken = refreshTokenRepository.save(refreshToken);
        return refreshToken;
    }

    public RefreshToken verifyExpiration(RefreshToken token) {
        if (token.getExpiryDate().isBefore(Instant.now())) {
            refreshTokenRepository.delete(token);
            throw new RuntimeException("Refresh token was expired. Please login again.");
        }
        return token;
    }

    public void deleteByUserId(Long userId) {
        User user = userRepository.findById(userId).get();
        refreshTokenRepository.deleteByUser(user);
    }
}

```

## Step 4: Modify Login Controller to Create and Send Refresh Token Cookie

In your authentication login endpoint, after generating the access JWT, create a refresh token and send it as an HttpOnly, Secure cookie:
```java
@PostMapping("/signin")
public ResponseEntity<?> authenticateUser(@Valid @RequestBody LoginRequest loginRequest, HttpServletResponse response) {
    Authentication authentication = authenticationManager.authenticate(
            new UsernamePasswordAuthenticationToken(loginRequest.getUsername(), loginRequest.getPassword()));
    SecurityContextHolder.getContext().setAuthentication(authentication);
    UserDetailsImpl userDetails = (UserDetailsImpl) authentication.getPrincipal();

    String jwt = jwtUtils.generateJwtToken(userDetails);
    RefreshToken refreshToken = refreshTokenService.createRefreshToken(userDetails.getId());

    Cookie refreshTokenCookie = new Cookie("refreshToken", refreshToken.getToken());
    refreshTokenCookie.setHttpOnly(true);
    refreshTokenCookie.setSecure(true); // Set true in production with HTTPS 
    refreshTokenCookie.setPath("/");
    refreshTokenCookie.setMaxAge(refreshTokenDurationMs.intValue() / 1000);
    response.addCookie(refreshTokenCookie);

    return ResponseEntity.ok(new JwtResponse(jwt, userDetails.getId(), userDetails.getUsername(), userDetails.getEmail()));
}

```

## Step 5: Create Refresh Token Endpoint

Endpoint for client to request new access token by sending refresh token cookie automatically:
```java
@PostMapping("/refreshtoken")
public ResponseEntity<?> refreshToken(HttpServletRequest request, HttpServletResponse response) {
    Cookie[] cookies = request.getCookies();
    if (cookies == null) {
        return ResponseEntity.badRequest().body("Refresh Token cookie is missing");
    }
    String refreshTokenStr = Arrays.stream(cookies)
        .filter(cookie -> "refreshToken".equals(cookie.getName()))
        .findFirst()
        .map(Cookie::getValue)
        .orElse(null);

    if (refreshTokenStr == null) {
        return ResponseEntity.badRequest().body("Refresh Token cookie is missing");
    }

    RefreshToken refreshToken = refreshTokenService.findByToken(refreshTokenStr)
        .orElseThrow(() -> new RuntimeException("Refresh token not found"));

    refreshTokenService.verifyExpiration(refreshToken);
    String token = jwtUtils.generateTokenFromUsername(refreshToken.getUser().getUsername());

    return ResponseEntity.ok(new TokenRefreshResponse(token));
}

```

## Step 6: Logout Endpoint to Clear Refresh Token Cookie
```java
@PostMapping("/signout")
public ResponseEntity<?> logoutUser(HttpServletResponse response) {
    Cookie deleteCookie = new Cookie("refreshToken", null);
    deleteCookie.setHttpOnly(true);
    deleteCookie.setSecure(true);
    deleteCookie.setPath("/");
    deleteCookie.setMaxAge(0); // delete immediately
    response.addCookie(deleteCookie);
    return ResponseEntity.ok("You've been signed out!");
}

```

## Step 7: Properties

Add to your `application.properties` or `application.yml`

```text
app.jwtSecret=yourSecretKey 
app.jwtExpirationMs=3600000 
app.jwtRefreshExpirationMs=86400000
```