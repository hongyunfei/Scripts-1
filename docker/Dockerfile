FROM python:alpine
LABEL maintainer="hongyunfei <hongyunfei1220@gmail.com>"
LABEL version="v1.4.0"
ENV PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin \
    HOME=/root \
    LANG=zh_CN.UTF-8 \
    SHELL=/bin/bash \
    PS1="\u@\h:\w \$ " \
    SCRIPTS_DIR="/Scripts"
COPY entrypoint.sh /usr/local/bin/entrypoint.sh
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories \
    && apk update -f \
    && apk upgrade \
    && apk --no-cache add -f bash \
                             coreutils \
                             git \
                             tzdata \
                             gcc \
                             musl-dev \
                             libxslt-dev \
    && rm -rf /var/cache/apk/* \
    && ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo "Asia/Shanghai" > /etc/timezone \
    && pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple \
    && python -m pip install --upgrade pip \
    && git clone -b master https://github.com/hongyunfei/Scripts-1 ${SCRIPTS_DIR} \
    && cd ${SCRIPTS_DIR} \
    && pip install -r requirements.txt \
    && chmod +x /usr/local/bin/entrypoint.sh
WORKDIR ${SCRIPTS_DIR}
ENTRYPOINT entrypoint.sh
