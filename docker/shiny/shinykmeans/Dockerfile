FROM rocker/shiny
MAINTAINER "The pbdR Core Team" RBigData@gmail.com

ENV SHINY_PATH /srv/shiny-server
COPY server.r ${SHINY_PATH}
COPY ui.r ${SHINY_PATH}

CMD ["/usr/bin/shiny-server.sh"]
