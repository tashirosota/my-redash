[app create]
heroku login
heroku create peep-redash --team=peep 
[addonの追加]
heroku addons:create heroku-postgresql:hobby-dev -a peep-redash 
heroku addons:create rediscloud:30 -a peep-redash 
heroku addons:create sendgrid:starter -a peep-redash
[config]
heroku config:set PYTHONUNBUFFERED=0 -a peep-redash 
heroku config:set QUEUES=queries,scheduled_queries,celery -a peep-redash 
heroku config:set REDASH_COOKIE_SECRET=YOUR_SECRET_TOKEN -a peep-redash 
heroku config:set REDASH_DATABASE_URL=$(heroku config:get DATABASE_URL) -a peep-redash 
heroku config:set REDASH_LOG_LEVEL=INFO -a peep-redash 
heroku config:set REDASH_REDIS_URL=$(heroku config:get REDISCLOUD_URL) -a peep-redash 
heroku config:set REDASH_HOST=YOUR_DOMAIN_URL -a peep-redash 
heroku config:set REDASH_MAIL_PASSWORD=YOUR_ADDON_PASSWORD -a peep-redash 
heroku config:set REDASH_MAIL_PORT=587 -a peep-redash 
heroku config:set REDASH_MAIL_SERVER=YOUR_ADDON_DOMAIN -a peep-redash 
heroku config:set REDASH_MAIL_USERNAME=YOUR_ADDON_USERNAME -a peep-redash 
heroku config:set REDASH_MAIL_USE_TLS=true -a peep-redash 
heroku config:set REDASH_MAIL_DEFAULT_SENDER=YOUR_MAIL_ADDRESS  -a peep-redash 
heroku config -a peep-redashで変数がすべて入っていることを確認。なければ追加する
[container push]
heroku container:login
heroku container:push  --recursive -a peep-redash web
heroku container:push --recursive -a peep-redash worker
heroku container:release web worker -a peep-redash 
[create db]
heroku run /app/manage.py database create_tables -a peep-redash
 [Enable worker dyno]
heroku ps:scale worker=1 -a peep-redash
[shell]
heroku run /bin/bash -a peep-redash 
