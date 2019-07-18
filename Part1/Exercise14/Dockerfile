FROM ruby:2.6.0
EXPOSE 3000

RUN apt-get update && apt-get install -y git curl
RUN git clone https://git@github.com/docker-hy/rails-example-project.git
WORKDIR /rails-example-project

RUN curl -sL https://deb.nodesource.com/setup_10.x | bash
RUN apt-get install -y  nodejs

RUN gem install bundler
RUN bundle install
RUN rails db:migrate
CMD rails s
