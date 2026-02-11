---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - JavaScript
note type: Informational Note
---
- AWS Free tier: **free deployment** 
**Tools**:
- *PM2* - Process Manager 
	- Automatic restart
	- Monitoring
- *Nginx*
	- reverse proxi server
	- Scalability
	- Enables HTTPS 
- *gZip*
	- compression tool
	- reduce loading time 
	- efficient bandwidth
- *winston*
	- logging library
	- monitoring performance 

### Optimizing Application
- Set `NODE_ENV` to production.
	- caching view templates
	- caching css files 
	- generating less error messages

We can use `dotenv` module to set those variables.
We create a `.env` file and set there:
```json
NODE_ENV=production
PORT=3000
farewheels_jwtSecretKey=mySecureKey
```

Also, it is necessary to import it in config module.

We need to modify the `server.js` file from `initialize` folder:
```JavaScript
const { logger } = require('./logging');  

module.exports = function (app) {
  const port = process.env.PORT || 3000;
  app.listen(port, () => logger.info(`Listening on port ${port}...`));

  if (process.env.NODE_ENV === 'production') {
    logger.info("App is running in production mode");
  } else {
    logger.info("App is running in development mode");
  }
};
```

### gZip
Create a `gzip.js` file in initialize folder:
```JavaScript
const compression = require('compression');

module.exports = function () {
  app.use(compression);
};
```

and `index.js`:
```JavaScript
require('./initialize/gzip')(app);
```

### PM2
1. `npm i pm2 -g`
2. `pm2 start index.js --name "farewheels-app"`
3. ![[Pasted image 20250507131044.png]]
- use `pm2 status` to see the status of the app
- `pm2 restart index.js --watch --name "farewheels-app"`  - restarts the app every time an error occurs

1. We need to install pm2 package from github
2. Then we need to run `npm run configure` in the directory where it was installed 
3. Now PM2 is running in the background

#### Clustering 
`pm2 start index.js -i max --name "farewheels-cluster"` to enable clustering 
It is used for multicore utilization:
![[Pasted image 20250507131624.png]]

### Caching with Nginx
- Download it from the website 
- Add the path of the nginx folder in env variables
- `nginx -v` to see its version
Modify the `nginx.config` file:
```
    proxy_cache_path /data/nginx/cache levels=1:2 keys_zone=mychache:10m max_size=10g inactive=60m use_temp_path=off

    server {
        listen 80;

        location / {
            proxy_cache mychache
            proxy_cache_valid 200 302 10m;
            proxy_cache_valid 404 1m;

            proxy_path http://localhost:3000;

            proxy_cache_use_stale error timeout invalid_header updating http_500 http_502 http_503 http_504;
            add_header X-Cache-Status $upstream_cache_status;
    }
```

Reduces the load time, response time 

**Load Balancer**:
Used for distribution of the incoming request efficiently, this enhances scalability and ensure high availability.
Modify the `nginx.config`:
```
server {
        listen 80;

        location / {
            proxy_cache mycache;
            proxy_cache_valid 200 302 10m;
            proxy_cache_valid 404 1m;

            proxy_pass http://app_servers;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;

            proxy_cache_use_stale error timeout invalid_header updating http_500 http_502 http_503 http_504;
            add_header X-Cache-Status $upstream_cache_status;
        }    
    }
```

**Reverse Proxy**:
- Error handling 
- caching 
- serve static files 

We modify the `nginx.config`:
```
...
			error_page 500 502 503 504 /custom_50x.html;
            cilent_max_body_size 10M;

            proxy_cache_use_stale error timeout invalid_header updating http_500 http_502 http_503 http_504;
            add_header X-Cache-Status $upstream_cache_status;
        }    

        location /static/ {
            root /path/to/static/files;
        }
...
```

then `nginx -s reload`


### Enhancing App Security
Freedomain.one 
We need to get SSL and TLS certificates.
Then modify the `nginx.config` file:
```
server {
	listen 443 ssl;
	server_name farewheels.run.place;

	ssl_certificate path/to/ssl;
	ssl_certificate_key pth/to/key;
}
```

We need to create another server block on line 70:
```
server {
	listen 80;
	server_name farewheels.run.place;

	return 301 https://%host$request_uri;
}
```

Restart nginx.

Now, we can defend our server from ddos attacks with limiting the number of requests user can make:
```
limit_req_zone $binary_remote_addr zone=mylimit:10m rate=10r/s;

...

location / {
	limit_req zone=mylimit burst=20;
	...
}
```

Restart nginx.


### Security best practices 
Add security header:
```
server {
	location / {
		...
		add_header X-Frame-Options "DENY";
		add_header X-Content-Type-Options "nosniff";
		add_header X-XSS-Protection "1; mode=block";
	}
}
```
save and restart.

```
location / {
	if ($request_method !~ ^(GET|POST|HEAD) {
		return 405;
	})
}
```

We need to `npm i helmet`