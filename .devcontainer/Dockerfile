# Isolated dev container for the portproxy portfolio site.
# Used together with .devcontainer/devcontainer.json in VS Code.
FROM ruby:3.2

LABEL org.opencontainers.image.description="Jekyll dev container for the isolated portproxy portfolio site"

# System build deps needed to compile native extensions (nokogiri, etc.)
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
       build-essential \
       nodejs \
       git \
       curl \
    && rm -rf /var/lib/apt/lists/*

# Non-root user matching the default UID of the container OS (1000)
RUN useradd -m -u 1000 -s /bin/bash vscode

WORKDIR /workspace

# Install Jekyll + needed gems globally so `bundle install` in the project is fast
RUN gem install jekyll bundler && gem update --system

USER vscode

EXPOSE 4000

# Default: preview the site (override with jekyll build for production checks)
CMD ["jekyll", "serve", "--host", "0.0.0.0", "-w"]