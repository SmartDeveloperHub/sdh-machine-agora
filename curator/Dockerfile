FROM alejandrofcarrera/phusion.python
MAINTAINER Alejandro F. Carrera

ENV HOME /usr/lib/sdhcurator

# Create directories & virtual env
RUN virtualenv $HOME/.env
WORKDIR /usr/lib/sdhcurator

# Configure runit
ADD ./my_init.d/ /etc/my_init.d/
ONBUILD ./my_init.d/ /etc/my_init.d/

CMD ["/sbin/my_init"]

VOLUME ["/usr/lib/sdhcurator"]
