# cakephp docker file
## docker container
コンテナを起動します。

    ~~~
    cd /docker/cake
    docker-compose up
    ~~~
   
ホストから各コンテナへは下記でアクセスします。

  ~~~
    docker exec -it cake_php bash
    docker exec -it cake_db bash
    docker exec -it cake_nginx sh
  ~~~
  
  CakePHPアプリ作成
  
   ~~~
    [host]
    docker exec -it cake_php bash
    [container]
    cd /var/www/html
    composer create-project --prefer-dist cakephp/app .
  ~~~
  データベースの接続情報を変更
  ~~~
    vi /var/www/html/config/app.php
  Datasources を変更します。
  変更箇所抜粋
  'Datasources' => [
  'host' => '172.26.0.4', ※docker-compose.ymlで指定したMySQLのアドレス
  'username' => 'admin',
  'password' => 'admin',
  'database' => 'cake',
  ]
  ~~~
  ブラウザに http://ホストのIP:8080 でアクセスすると、 welcomeページが表示され、データベース接続もされていることが確認できます。

やはりDockerは楽で良いですね。
##Source:
~~~
http://bashalog.c-brains.jp/19/06/26-145446.php
~~~
