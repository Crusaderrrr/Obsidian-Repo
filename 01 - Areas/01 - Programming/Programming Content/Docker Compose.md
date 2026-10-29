`docker-compose.yml` file is used to orchestrate many docker images, e.g. frontend + backend + db and join them into single system.

```yaml
services:
  frontend:
    image: nginx:alpine
    ports:
      - "80:80"
    networks:
      - public
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf:ro   # bind mount, read-only

  app:
    build: .
    depends_on:
	    db:
		    condition: service_healthy
    networks:
      - public
      - private
    ports:
	    - "8080:8080" # host 8080 → container 8080 
	    - "9000:8080" # host 9000 → container 8080
	    - "127.0.0.1:5432:5432" # reachable only from my machine, not the LAN 
	    - "8080" # container 8080 → random free host port 
	    - "53:53/udp" # UDP instead of the default TCP

  db:
    image: postgres:16
    environment:
      POSTGRES_PASSWORD: secret  # specify environment variable
    networks:
      - private
    volumes:
      - pgdata:/var/lib/postgresql/data       # named volume
    healthcheck: 
	    test: ["CMD-SHELL", "pg_isready -U postgres -d mydb"] 
	    interval: 5s 
	    timeout: 3s 
	    retries: 5 
	    start_period: 10s

networks:
  public:
  private:
    internal: true

volumes:
  pgdata:
```

- **services** - containers to run
- `build .` - builds a file from the current directory where compose lives
- **depends_on**  - starts the dependencies first 
- **volumes** - keeps data outside the container. The top-level `volumes:` declares a named volume, and the service-level entry mounts it at Postgres’s data directory. Without it, your database is wiped whenever the container is removed.
- **networks**
	- **Default behaviour:** without any `networks:` keys, Compose puts every service on one shared network. That’s enough for most setups.
	- **Top-level `networks:`** declares the networks. An empty entry like `public:` gives you a default bridge network.
	- **Service-level `networks:`** lists the networks a service joins. Services can talk only if they share at least one network, using the service name as the hostname.
	- **In this example:** `frontend` can reach `app` but not `db`. `app` sits on both networks and acts as the bridge. `internal: true` also cuts `private` off from the internet.
- **healthcheck**
	- `test` is the command to run
	- interval - how often runs
	- timeout - how long a check can run for, before it is counted as failed
	- retries - times a healthcheck retries
	- `start_period` - first healthcheck runs after specified time after startup
	- `condition` - a condition to start the container

### Commands
- `docker compose up -d` - build if needed, start everything in the background
- `docker compose logs -f app` - show all the existing logs and stream new ones 
- `docker compose down` - stops the full service
- `docker compose ps` - show all services and some info (health, ports, names, etc.)