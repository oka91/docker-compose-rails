# 説明
Railsのソースコードを動かす環境をDockerコンテナで構築する。ソースコードのディレクトリ名は必ずsrcとする。

# srcが既にある場合
1. srcディレクトリをdocker-compose.ymlと同じディレクトリに配置
2. gem 'mysql2', '>= 0.4.4', '< 0.6.0'をGemfileに追記 : DBコンテナにはmariadbを使っているため必要
3. docker-compose up -d
4. docker exec -it rails-container rails db:create : DBの作成
5. docker exec -it rails-container rails db:migrate : マイグレーションの実行

# srcがない場合(新規プロジェクトの場合)は下記手順で作成
1. docker container run -it -v $PWD/src:/rails-src oka9111/ruby-2.6.0-rails-base /bin/sh
2. gem install rails : コンテナ内の作業。若干時間がかかる
3. rails new rails-src --database=mysql --skip-bundle : コンテナ内の作業
4. exit
5. docker-compose up -d : 最初はDockerImageがビルドされる過程でbundle installを行うので時間がかかる
6. docker exec -it rails-container rails db:create : DBの作成

http://localhost:8080にアクセスすればrailsのルートドキュメントにつながる
http://localhost:8000にアクセスすればphpmyadminでmariadbをGUIで確認できる

docker-compose.ymlでコメントアウトされているselenium-chromeコンテナはE2Eテストでブラウザが必要な場合に使用する。これがあればテスト時にGoogle Chrome本体やchromedriverをインストールする必要がない
