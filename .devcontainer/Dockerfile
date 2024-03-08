# Jekyll 開発環境
#   VS Code 開発コンテナーを使用したJekyllによるドキュメント開発環境
#
FROM ruby:latest

# 環境変数
ENV DEBIAN_FRONTEND=noninteractive \  
    LANG=ja_JP.UTF-8 \
    LANGUAGE=ja_JP:ja \ 
    TZ=Asia/Tokyo

# パッケージインストール
RUN apt-get update && \
    apt-get install --no-install-recommends -y \
    locales \
    sudo \
    vim \
    git \
    iputils-ping \
    iproute2 \
    openssh-client \
    && \
# ロケールの生成
    localedef -f UTF-8 -i ja_JP ja_JP.UTF-8 \
    && \
# Clean up
    apt-get clean && \
    rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*

# sudo可能な一般ユーザーを追加
ARG USERNAME=user
ARG GROUPNAME=user
ARG UID=1000
ARG GID=1000
ARG PASSWORD=user
RUN groupadd -g $GID $GROUPNAME && \
    useradd -m -s /bin/bash -u $UID -g $GID -G sudo $USERNAME && \
    echo $USERNAME:$PASSWORD | chpasswd && \
    echo "$USERNAME   ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers
USER $USERNAME

# 作業ディレクトリを設定
WORKDIR /home/$USERNAME

# jekyllのインストール
RUN gem install jekyll

# コンテナ起動時に実行するコマンド
CMD ["/bin/bash"]