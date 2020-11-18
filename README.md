

> db superuser

- root/rootでとりあえず開発中


- templates
    - [x] login後、custom pageに飛ぶ様に開発
    - [o] custom pageでデータをSSRし、jinjaで開発してもらえる様にする。
        - サクッと出来そう。
        https://qiita.com/takuto_neko_like/items/62aeb4271614f6f0347f

- development
    - data送信API実装
    - https://www.django-rest-framework.org/tutorial/1-serialization/
    - 次はここから
    - `curl -X PUT -H 'Content-Type:application/json' -d '{"title":"hello", "user_name":"hoge", "code":"world"}' http://localhost:9009/receive_censor_data/send/`

    - [o] DBにデータが格納されることを確認



- Deploy (11/18に実装予定)
    - [ ] HEROKU上でdocker起動できる様にする
    https://qiita.com/hagyyyy1992/items/466b5bab67118175be65 
    - [ ] volumeを使える様にする。

- テスト
    - [ ] postでデータを送信できることを確認する。

- 追加開発
    - [ ] LINE bot に異常時に通知がいく機能を追加する。

【開発メモ】

- dev環境で、依存関係無くpostgresqlを実装できる様にdockerを利用して開発する。
- docker compose でdebugできる。 
    - `docker-compose run web python manage.py makemigrations home_monitoring`
    - `docker-compose run << CONTAINER_NAME >> command`
    - `docker exec -it dev_db_1 psql -U postgres`
    - micro service architecture開発が捗る



- https://devcenter.heroku.com/articles/build-docker-images-heroku-yml

```
setup - Specifies the add-ons and config vars to create during app provisioning
build - Specifies the Dockerfile to build
release - Specifies the release phase tasks to execute
run - Specifies process types and the commands to run for each

```

`The python application depends on Postgres and Redis, which you do not push to Heroku. Instead, use Heroku add-ons in production.`


add-onsを利用する。heroku config に DATABASE_URLが追加される
→settings.pyに貼り付ける。
→heroku 上でdocker-composeを使う方法がわからなかった \& portの複数利用の方法がわからなかったため、microservice architectureをあきらめ、API/WEBサーバを統一する方針に切り替える。






