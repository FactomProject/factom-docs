FROM ruby:2.3.3

RUN apt-get update \
    && apt-get install -y nodejs \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*  /tmp/* /var/tmp/*

RUN mkdir -p /usr/src/app

WORKDIR /usr/src/app

COPY config.rb font-selection.json Gemfile Gemfile.lock /usr/src/app/

RUN bundle install

CMD ["bundle", "exec", "middleman", "server", "--watcher-force-polling"]

EXPOSE 8000 8001