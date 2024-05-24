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
# 2024/05/24 追記
# rye のダウンロード先が変更
# ref: [gitリポジトリのReadme](https://github.com/astral-sh/rye)
# 2024/05/24 追記
# RYE_INSTALL_OPTION="--yes" がない場合、インストールエラー
# ref: [Error: IO error: not a terminal #246](https://github.com/astral-sh/rye/issues/246)
RUN curl -sSf https://rye.astral.sh/get | RYE_INSTALL_OPTION="--yes" bash && \
  echo 'source "$HOME/.rye/env"' >> ~/.bashrc

# 不要なパッケージの削除
RUN apt-get autoremove -y && \
  apt-get -y clean && \
  rm -rf /var/lib/apt/lists/*
