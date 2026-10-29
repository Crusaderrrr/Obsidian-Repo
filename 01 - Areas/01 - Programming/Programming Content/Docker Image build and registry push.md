This is an **example flow of how to build and push and image to public registry**.
```bash
# 1. Build: package your app (needs a Dockerfile in the current dir)
docker build -t myapp:1.0 .

# 2. Tag: put the registry address on the label
docker tag myapp:1.0 <registry>/<namespace>/myapp:1.0
#   Docker Hub:  yourusername/myapp:1.0         (host is implied)
#   GHCR:        ghcr.io/yourusername/myapp:1.0
#   AWS ECR:     <acct>.dkr.ecr.<region>.amazonaws.com/myapp:1.0

# 3. Log in to that registry
docker login                 # Docker Hub
docker login ghcr.io         # GitHub (username + PAT with write:packages)

# 4. Push
docker push <registry>/<namespace>/myapp:1.0
```

- `docker build` - command to build docker image (`-t` tag is used to target which image we want to build, `.` means current directory)