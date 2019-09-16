FROM php:7.2-fpm

# 设置时区
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# 更新安装依赖包和PHP核心拓展
RUN apt-get update && apt-get install -y \
        git \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install zip \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install opcache \
    && docker-php-ext-install mysqli \
    && rm -r /var/lib/apt/lists/*


# 安装 PECL 拓展，这里我们安装的是redis psr
# 最新的phalcon扩展,需要 psr
RUN pecl install redis-5.0.2 \
    && pecl install psr \
    && docker-php-ext-enable redis psr

# 安装第三方拓展，这里是 Phalcon 拓展
RUN cd /home \
    && git clone --depth=1 git://github.com/phalcon/cphalcon.git \
    && cd cphalcon/build \
    && ./install \
    && echo "extension=phalcon.so" > /usr/local/etc/php/conf.d/phalcon.ini \
    && rm -rf /home/*

# 添加配置文件,新添加的phalcon项目需要
COPY idc.ini /data/app/idc/idc.ini

WORKDIR /data


