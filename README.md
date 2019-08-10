# SvnserverOnDocker

# docker-hub svn-serverページ
https://hub.docker.com/r/garethflowers/svn-server/builds

# イメージのダウンロード
sudo docker pull garethflowers/svn-server

# docker-compose.ymlの編集
vi docker-compose.yml
svn:
  image: garethflowers/svn-server:latest
  container_name: svnserver
  restart: always
  volumes:
     - ./svn:/var/opt/svn 
  ports:
     - 3690:3690

# コンテナの作成
sudo docker-compose up -d

# コンテナにログイン※alpineの場合
sudo docker exec -it svnserver /bin/ash

# リポジトリを作成
svnadmin create svn

# svnの設定を変更
http://svn.linux-dvr.biz/archives/149

cp ./svn/conf/svnserve.conf ./svn/conf/svnserve.conf_bak
vi ./svn/conf/svnserve.conf
[general]
# 匿名アクセスを許可するかどうかを設定する。(read,write,none)
anon-access = read
# 認証されたユーザーのアクセス権を設定する。(read,write,none)
auth-access = write
# ユーザーとパスワードが記述されたファイルへのパスを指定する。
password-db = passwd 
#ディレクトリ・ファイル単位(リポジトリ内)のアクセス権が記述されたファイルへのパスを指定する。
#authz-db = authz

cp ./svn/conf/passwd ./svn/conf/passwd_bak
vi ./svn/conf/passwd.conf
[users]
ユーザー = パスワード

# クライアントよりアクセス
svn://192.168.100.105/svn
