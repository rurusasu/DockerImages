ARG BASE_IMAGE=ubuntu:latest
FROM ${BASE_IMAGE}

# パッケージインストール
RUN apt-get update && \
  apt-get install --no-install-recommends -y \
  build-essential \
  cmake \
  curl \
  git \
  sudo \
  libpython3-dev \
  wget \
  gnupg \
  unzip \
  # curl: (77) error setting certificate verify locations への対策
  # ref: https://askubuntu.com/questions/1390288/curl-77-error-setting-certificate-verify-locations-ubuntu-20-04-3-lts
  ca-certificates

# Rye のインストールと環境設定
SHELL [ "/bin/bash", "-o", "pipefail", "-c" ]
#RUN curl -sSf https://rye.astral.sh/get | RYE_INSTALL_OPTION="--yes" bash
RUN mkdir -p /opt/rye && curl -sSf https://rye.astral.sh/get | RYE_INSTALL_OPTION="--yes" bash -s -- --prefix /opt/rye
ENV RYE_HOME="/opt/rye"
ENV PATH="$RYE_HOME/shims:$PATH"
RUN chown -R root $RYE_HOME
# rye config --set-bool behavior.global-python=true && \
# rye config --set-bool behavior.use-uv=true


# ChromeとChromeDriverのバージョン指定
ENV CHROME_VERSION=125.0.6422.78
ENV CHROMEDRIVER_VERSION=125.0.6422.78

# ChromeとChromeDriverのインストール
RUN curl -Lo "/tmp/chrome-linux64.zip" "https://storage.googleapis.com/chrome-for-testing-public/$CHROME_VERSION/linux64/chrome-linux64.zip" && \
  curl -Lo "/tmp/chromedriver-linux64.zip" "https://storage.googleapis.com/chrome-for-testing-public/$CHROMEDRIVER_VERSION/linux64/chromedriver-linux64.zip" && \
  unzip /tmp/chrome-linux64.zip -d /opt/ && \
  unzip /tmp/chromedriver-linux64.zip -d /opt/ && \
  mv /opt/chrome-linux64 /opt/chrome && \
  ln -s /opt/chrome/chrome /usr/bin/google-chrome && \
  mv /opt/chromedriver-linux64 /usr/local/bin/chromedriver && \
  rm /tmp/chrome-linux64.zip /tmp/chromedriver-linux64.zip

# 不要なパッケージの削除
#RUN apt-get autoremove -y && \
#  apt-get -y clean && \
#  rm -rf /var/lib/apt/lists/*

# 作業ディレクトリの設定
WORKDIR /workspace

#RUN useradd -m vscode

SHELL [ "/bin/bash" ]