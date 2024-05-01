ARG BASE_IMAGE=ubuntu:latest
FROM ${BASE_IMAGE}

# パッケージインストール
RUN apt-get update && \
  apt-get install --no-install-recommends -y \
  sudo \
  curl \
  # curl: (77) error setting certificate verify locations への対策
  # ref: https://askubuntu.com/questions/1390288/curl-77-error-setting-certificate-verify-locations-ubuntu-20-04-3-lts
  ca-certificates

# Rye install
SHELL [ "/bin/bash", "-o", "pipefail", "-c" ]
RUN curl -sSf https://rye-up.com/get | RYE_INSTALL_OPTION="--yes" bash && \
  echo 'source "$HOME/.rye/env"' >> ~/.bashrc

# 不要なパッケージの削除
RUN apt-get autoremove -y && \
  apt-get -y clean && \
  rm -rf /var/lib/apt/lists/*
