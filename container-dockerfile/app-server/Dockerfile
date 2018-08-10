FROM oka9111/ruby-2.5.1-rails-5.2.0-base

# アプリケーションのデプロイ
ENV APP_HOME /var/www/rails-app
RUN mkdir -p $APP_HOME
ADD ./src $APP_HOME

# 依存パッケージのインストール
WORKDIR $APP_HOME
RUN bundle install

# Webサーバーの起動
CMD exec rails s -p 3000 -b '0.0.0.0'
