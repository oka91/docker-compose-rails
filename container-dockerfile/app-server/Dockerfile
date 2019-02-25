FROM oka9111/ruby-2.6.0-rails-base:latest

# アプリケーションのデプロイ
ENV APP_HOME /var/www/rails-app
RUN mkdir -p $APP_HOME
ADD ./src $APP_HOME

# 依存パッケージのインストール
WORKDIR $APP_HOME
RUN bundle install

# Pumaの起動はDockerComposeファイル内で行う
