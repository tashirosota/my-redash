# usage

## app create

```
heroku login
heroku create pAPP_NAME --team=TEAM_NAME
```

## addonの追加

```
heroku addons:create heroku-postgresql:hobby-dev -a APP_NAME
heroku addons:create rediscloud:30 -a APP_NAME 
heroku addons:create sendgrid:starter -a peep-redash
```

## config

```
heroku config:set PYTHONUNBUFFERED=0 -a APP_NAME
heroku config:set QUEUES=queries,scheduled_queries,celery -a APP_NAME
heroku config:set REDASH_COOKIE_SECRET=YOUR_SECRET_TOKEN -a APP_NAME
heroku config:set REDASH_DATABASE_URL=$(heroku config:get DATABASE_URL) -a APP_NAME 
heroku config:set REDASH_LOG_LEVEL=INFO -a APP_NAME
heroku config:set REDASH_REDIS_URL=$(heroku config:get REDISCLOUD_URL) -a APP_NAME
heroku config:set REDASH_HOST=YOUR_DOMAIN_URL -a APP_NAME
heroku config:set REDASH_MAIL_PASSWORD=YOUR_ADDON_PASSWORD -a APP_NAME
heroku config:set REDASH_MAIL_PORT=587 -a APP_NAME
heroku config:set REDASH_MAIL_SERVER=YOUR_ADDON_DOMAIN -a APP_NAME
heroku config:set REDASH_MAIL_USERNAME=YOUR_ADDON_USERNAME -a APP_NAME
heroku config:set REDASH_MAIL_USE_TLS=true -a APP_NAME
heroku config:set REDASH_MAIL_DEFAULT_SENDER=YOUR_MAIL_ADDRESS  -a pAPP_NAME
heroku config -a APP_NAMEで変数がすべて入っていることを確認。なければ追加する
```

## container push

```
heroku container:login
heroku container:push  --recursive -a APP_NAME web
heroku container:push --recursive -a APP_NAME worker
heroku container:release web worker -a APP_NAME
```

## create db

```
heroku run /app/manage.py database create_tables -a APP_NAME
```

## Enable worker dyno

```
heroku ps:scale worker=1 -a APP_NAME
```

## shell

```
heroku run /bin/bash -a APP_NAMEME 
```
