ARG BASE_IMAGE=ubuntu:22.04
FROM ${BASE_IMAGE}

ARG PROJECT_NAME=Core
ARG USER_NAME=User
#ARG GROUP_NAME=challengers
#ARG UID=1000
#ARG GID=1000
ARG PYTHON_VERSION=3.11
ARG APPLICATION_DIRECTORY=/home/${USER_NAME}/${PROJECT_NAME}
ARG RUN_POETRY_INSTALL_AT_BUILD_TIME="false"
ARG CHROME_DRIVER_VERSION=114.0.5735.90

# 日本語化
USER root
RUN apt-get update \
  && apt-get install --no-install-recommends -y \
  fonts-noto-cjk \
  fonts-noto-cjk-extra \
  && apt-get install locales -y \
  # ja_JP.UTF-8の行のコメントを解除
  && sed -i -E 's/# (ja_JP.UTF-8)/\1/' /etc/locale.gen \
  && locale-gen \
  && update-locale LANG=ja_JP.UTF-8 \
  && apt-get clean \
  && rm -r /var/lib/apt/lists/*

ENV DEBIAN_FRONTEND="noninteractive" \
  TZ="Asia/Tokyo" \
  LC_ALL="ja_JP.UTF-8" \
  LANG="ja_JP.UTF-8" \
  LANGUAGE="ja_JP:ja" \
  PYTHONPATH=${APPLICATION_DIRECTORY}

# パッケージインストール
RUN apt update && apt install --no-install-recommends -y \
  sudo \
  wget \
  curl \
  gnupg \
  && apt-get clean \
  && rm -r /var/lib/apt/lists/*

# chrome driver
#ADD https://chromedriver.storage.googleapis.com/${CHROME_DRIVER_VERSION}/chromedriver_linux64.zip /opt/chrome/
#RUN cd /opt/chrome/ && \
#  unzip chromedriver_linux64.zip && \
#  rm -f chromedriver_linux64.zip

# Google Chrome Install
#RUN sudo sh -c 'echo "deb https://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list' && \
#  wget -q -O - https://dl.google.com/linux/linux_signing_key.pub | sudo apt-key add - && \
#  apt-get update && \
#  apt-get install -y google-chrome-stable && \
#  apt-get -y clean && \
#  rm -rf /var/lib/apt/lists/*

# Python Install
RUN python3 -m pip install --upgrade pip setuptools requests \
  && python3 -m pip install poetry \
# Poetry が作成する仮想環境のディレクトリをプロジェクト直下に変更
# Ref: [Poetry documentation (ver. 1.1.6 日本語訳)]
# (https://cocoatomo.github.io/poetry-ja/configuration/)
  && poetry config virtualenvs.in-project true

# Add user. Without this, following process is executed as admin.
#RUN groupadd -g ${GID} ${GROUP_NAME} \
#  && useradd -ms /bin/sh -u ${UID} -g ${GID} ${USER_NAME}

#USER ${USER_NAME}
WORKDIR ${APPLICATION_DIRECTORY}

# If ${RUN_POETRY_INSTALL_AT_BUILD_TIME} = "true", install Python package by Poetry and move .venv under ${HOME}.
# This process is for CI (GitHub Actions). To prevent overwrite by volume of docker compose, .venv is moved under ${HOME}.
#COPY --chown=${UID}:${GID} pyproject.toml poetry.lock poetry.toml .
#RUN test ${RUN_POETRY_INSTALL_AT_BUILD_TIME} = "true" && poetry install || echo "skip to run poetry install."
#RUN test ${RUN_POETRY_INSTALL_AT_BUILD_TIME} = "true" && mv ${APPLICATION_DIRECTORY}/.venv ${HOME}/.venv || echo "skip to move .venv."
