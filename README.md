# docker-django-sample-2
Djangoとはを知るためにチュートリアルアプリを作成しました。  
環境をDockerにしているところ以外は下記サイトの通りです。  
https://docs.djangoproject.com/ja/1.9/intro/tutorial01/

## 初回設定
１．適当なフォルダにクローン
```bash
git clone https://github.com/satokourov/docker-django-sample-2.git
```

２．フォルダを移動してdocker-composeを起動
```bash
cd docker-django-sample-2/
docker-compose up -d
```

３．コンテナが起動している事を確認（webとmysqlが起動しているはず）
```bash
docker ps
```

４．mysqlコンテナにログインして起動
```bash
docker exec -it mysql bash
```

５．mysqlにログインしデータベースを作成
　※今回は「mysite」というDBを作成
　※mysqlコンテナにログインした状態で実行
```bash
mysql -p
(pass)
create database mysite CHARACTER SET utf8;
```

６．webコンテナにログイン
```bash
docker exec -it web bash
```

７．「５」で作ったデータベースにテーブルを作る
　※webコンテナにログインした状態で実行
　※Djangoプロジェクトは「/code」にあります
```bash
cd /code/
python manage.py migrate
```

８．サーバを起動
　※ホスト側で実行
```bash
docker-compose restart
```

９．管理サイトに入るアカウントを設定
　※webコンテナにログインして作成
```bash
docker exec -it web bash
cd /code/ 
python manage.py createsuperuser
$ Username (leave blank to use 'root'): #任意
$ Email #任意
$ Password: #任意
$ Password (again): #再入力
```

１０．管理画面にアクセス
http://localhost/admin/login/
※先ほど設定したID/PASSでログイン出来ます
POLLSというのがサンプルアプリになります。Questionsテーブルに何か追加してください。

１１．アプリ画面にアクセス
http://localhost/polls/
管理画面で登録した内容が表示されているはずです。
