FROM php:latest

# install base packages
RUN \
  apt-get update && apt-get install -y \
  subversion \
  wget

# install pear
WORKDIR /tmp
RUN wget http://pear.php.net/go-pear.phar && php go-pear.phar

# install phd
RUN \
  pear install doc.php.net/phd && \
  pear install doc.php.net/phd_ide-1.1.1

# checkout phpdoc
RUN svn co http://svn.php.net/repository/phpdoc/modules/doc-en /home/phpdoc

# configure phpdoc
WORKDIR /home/phpdoc
RUN php doc-base/configure.php

CMD ["phd", "-d", "doc-base/.manual.xml", "-P", "IDE", "--format", "json"]
