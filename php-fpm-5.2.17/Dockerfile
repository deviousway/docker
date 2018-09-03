FROM centos:6
RUN yum  update -y && yum clean all
RUN yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-6.noarch.rpm -y
RUN yum install wget -y
RUN yum whatprovides *mcrypt.h
WORKDIR /tmp
RUN /usr/bin/wget  http://museum.php.net/php5/php-5.2.17.tar.gz
RUN /usr/bin/wget  https://php-fpm.org/downloads/php-5.2.17-fpm-0.5.14.diff.gz
RUN yum install -y wget patch gcc libtool libmcrypt-devel libxml2-devel flex bison make pcre-devel zlib-devel openssl-devel gd-devel libtool-ltdl-devel mysql-devel libmcrypt-devel
RUN tar -xvpf php-5.2.17.tar.gz
RUN gzip -cd php-5.2.17-fpm-0.5.14.diff.gz | patch -d php-5.2.17 -p1
WORKDIR /tmp/php-5.2.17/
RUN  ./configure --prefix=/usr/local/php5217 --enable-fastcgi --enable-fpm --enable-cli --with-mcrypt --with-zlib --enable-mbstring --with-openssl --with-mysql --with-mysql-sock --with-gd --with-jpeg-dir=/usr/lib64 --enable-gd-native-ttf --without-sqlite --disable-pdo --with-libdir=lib64 --with-xpm-dir=/usr/lib64 --enable-gd-jis-conv --with-freetype-dir=/usr/include/freetype2 --with-fpm-user=apache --with-fpm-group=apache --enable-shared
RUN make all install
RUN strip /usr/local/php5217/bin/php-cgi
