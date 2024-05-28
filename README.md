#### (Since deadly bullboard is not maintained now, this repo contains the `5.6.0` version of bullboard/ui and bullboard/api changes 🎉, along with that some ui configs options are added as env variable which enables ui to be configured ✨)

Docker image for [bull-board]. Allow you to monitor your bull queue without any coding!

Supports both: bull and bullmq. bull-board version v3.2.6

### Quick start with Docker
```
docker run -p 3000:3000 kunwarsaab/bull-board
```
will run bull-board interface on `localhost:3000` and connect to your redis instance on `localhost:6379` without password.

To configurate redis see "Environment variables" section.

### Quick start with docker-compose
```yaml
version: '3.5'

services:
  bullboard:
    container_name: bullboard
    image: kunwarsaab/bull-board
    restart: always
    ports:
      - 3000:3000
```
will run bull-board interface on `localhost:3000` and connect to your redis instance on `localhost:6379` without password.

see "Example with docker-compose" section for example with env parameters


### Environment variables
* `REDIS_HOST` - host to connect to redis (localhost by default)
* `REDIS_PORT` - redis port (6379 by default)
* `REDIS_DB` - redis db to use ('0' by default)
* `REDIS_USE_TLS` - enable TLS true or false (false by default)
* `REDIS_PASSWORD` - password to connect to redis (no password by default)
* `BULL_PREFIX` - prefix to your bull queue name (bull by default)
* `BULL_VERSION` - version of bull lib to use 'BULLMQ' or 'BULL' ('BULLMQ' by default)
* `PROXY_PATH` - proxyPath for bull board, e.g. https://<server_name>/my-base-path/queues [docs] ('' by default)
* `USER_LOGIN` - login to restrict access to bull-board interface (disabled by default)
* `USER_PASSWORD` - password to restrict access to bull-board interface (disabled by default)
* `BOARD_TITLE`: text for changing the default title of the board,
*	`BOARD_LOGO` : url of logo to be used instead of default one,
*	`BOARD_WIDTH` : css for logo,
*	`BOARD_HEIGHT` : css for logo,
*	`FAVICON_DEFAULT` : default favicon, if configuration is needed,
*	`FAVICON_ALTERNATIVE` : alternative favicon, if configuration is needed,

### Restrict access with login and password

To restrict access to bull-board use `USER_LOGIN` and `USER_PASSWORD` env vars.
Only when both `USER_LOGIN` and `USER_PASSWORD` specified, access will be restricted with login/password


### Example with docker-compose
```yaml
version: '3.5'

services:
  redis:
    container_name: redis
    image: redis:5.0-alpine
    restart: always
    ports:
      - 6379:6379
    volumes:
      - redis_db_data:/data

  bullboard:
    container_name: bullboard
    image: kunwarsaab/bull-board
    restart: always
    ports:
      - 3000:3000
    environment:
      REDIS_HOST: redis
      REDIS_PORT: 6379
      REDIS_PASSWORD: example-password
      REDIS_USE_TLS: 'false'
      BULL_PREFIX: bull
    depends_on:
      - redis

volumes:
  redis_db_data:
    external: false
```

[bull-board]: https://github.com/vcapretz/bull-board
[bull-board]: https://github.com/felixmosh/bull-board#hosting-router-on-a-sub-path
