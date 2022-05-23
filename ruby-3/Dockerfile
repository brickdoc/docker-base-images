FROM ubuntu:22.04
ARG RUBY_VERSION="3.1-jemalloc"

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
  && curl -SLf https://raw.githubusercontent.com/fullstaq-labs/fullstaq-ruby-server-edition/main/fullstaq-ruby.asc |  gpg --dearmour -o /etc/apt/trusted.gpg.d/fullstaq.gpg \
  && echo "deb https://apt.fullstaqruby.org ubuntu-22.04 main" > /etc/apt/sources.list.d/fullstaq-ruby.list \
  && apt-get update -q \
  && apt-get install --assume-yes -q --no-install-recommends fullstaq-ruby-${RUBY_VERSION} \
  libcurl4-openssl-dev libpq-dev libxml2-dev libsodium23 libxslt-dev \
  && apt-get remove -y --purge gnupg apt-transport-https \
  && apt-get autoremove --assume-yes \
  && rm -rf /var/lib/apt/lists \
  && rm -fr /var/cache/apt \
  && rm /etc/apt/sources.list.d/fullstaq-ruby.list \
  && echo 'gem: --no-rdoc --no-ri' >> "$HOME/.gemrc"  && \
  bundle config set --global deployment 'true'

ENV GEM_HOME /usr/local/bundle
ENV BUNDLE_PATH="$GEM_HOME" \
    BUNDLE_SILENCE_ROOT_WARNING=1 \
    BUNDLE_APP_CONFIG="$GEM_HOME" \
    RUBY_VERSION=3.1 \
    LANG=C.UTF-8 LC_ALL=C.UTF-8

RUN gem install rake
CMD [ "irb" ]
