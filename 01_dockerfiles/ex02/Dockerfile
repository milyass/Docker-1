FROM ruby:2.6
RUN apt update && apt upgrade -y && apt install -y nodejs 
RUN gem install rails
COPY app /opt/app
WORKDIR /opt/app
ONBUILD EXPOSE 3000
ONBUILD RUN bundle install
ONBUILD RUN bundle exec rake db:setup
ONBUILD RUN bundle exec rake db:migrate