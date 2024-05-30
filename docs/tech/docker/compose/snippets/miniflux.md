# miniflux

```yaml
version: '3.4'
services:
  miniflux:
    image: ${MINIFLUX_IMAGE:-miniflux/miniflux:latest}
    container_name: miniflux
    restart: always
    ports:
      - "127.0.0.1:3000:8080"
    depends_on:
      - db
    environment:
      - DATABASE_URL=postgres://miniflux:secret@db/miniflux?sslmode=disable
      - RUN_MIGRATIONS=1
      - CREATE_ADMIN=1
      - ADMIN_USERNAME=admin
      - ADMIN_PASSWORD=mNiUv2nSKzXV8A
      - DEBUG=0
    # Optional health check:
    # healthcheck:
    #  test: ["CMD", "/usr/bin/miniflux", "-healthcheck", "auto"]
  db:
    image: postgres:latest
    container_name: postgres
    environment:
      - POSTGRES_USER=miniflux
      - POSTGRES_PASSWORD=secret
    volumes:
      - miniflux-db:/var/lib/postgresql/data
    healthcheck:
      test: ["CMD", "pg_isready", "-U", "miniflux"]
      interval: 10s
      start_period: 30s
volumes:
  miniflux-db:
```