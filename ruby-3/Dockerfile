FROM ubuntu:20.04
ARG RUBY_VERSION="3.0-jemalloc"

# RUN with pipe recommendation: https://github.com/hadolint/hadolint/wiki/DL4006
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

ENV BUNDLE_SILENCE_ROOT_WARNING=1 \
  RUBY_VERSION=${RUBY_VERSION} \
  LANG=C.UTF-8 LC_ALL=C.UTF-8

ENV PATH /usr/lib/fullstaq-ruby/versions/${RUBY_VERSION}/bin:$PATH

RUN apt-get update -q \
  && apt-get dist-upgrade --assume-yes \
  && apt-get install --assume-yes -q --no-install-recommends \
  curl \
  gnupg \
  apt-transport-https \
  ca-certificates \
  && curl -SLf https://apt.postgresql.org/pub/repos/apt/ACCC4CF8.asc | apt-key add - \
  && curl -SLf https://raw.githubusercontent.com/fullstaq-labs/fullstaq-ruby-server-edition/main/fullstaq-ruby.asc | apt-key add - \
  && echo "deb http://apt.postgresql.org/pub/repos/apt/ focal-pgdg main" > /etc/apt/sources.list.d/postgres.list \
  && echo "deb https://apt.fullstaqruby.org ubuntu-20.04 main" > /etc/apt/sources.list.d/fullstaq-ruby.list \
  && apt-get update -q \
  && apt-get install --assume-yes -q --no-install-recommends fullstaq-ruby-${RUBY_VERSION} \
  libcurl4-openssl-dev libpq-dev libxml2-dev libsodium-dev libxslt-dev\
  && apt-get remove -y --purge gnupg apt-transport-https \
  && apt-get autoremove --assume-yes \
  && rm -rf /var/lib/apt/lists \
  && rm -fr /var/cache/apt \
  && rm /etc/apt/sources.list.d/fullstaq-ruby.list \
  && rm /etc/apt/sources.list.d/postgres.list \
  && echo 'gem: --no-rdoc --no-ri' >> "$HOME/.gemrc"  && \
  bundle config set --global deployment 'true'

CMD [ "irb" ]
