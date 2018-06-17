FROM rocker/shiny
MAINTAINER "The pbdR Core Team" RBigData@gmail.com
ENV MAKE make -j 4

RUN apt-get update && apt-get install -y --no-install-recommends apt-utils r-cran-curl curl

RUN mkdir -p /R/lib

RUN echo " \
  .libPaths('/R/lib'); \
  options(repos=structure(c(CRAN='https://cran.rstudio.com/'))) ; \
  utils::rc.settings(ipck=TRUE);" > /usr/lib/R/etc/Rprofile.site

RUN rm -rf /usr/lib/R/site-library
RUN rm -rf /usr/local/lib/R/site-library

RUN r -e "install.packages('remotes')"
RUN r -e "install.packages(c('shiny', 'ggvis', 'dplyr', 'RSQLite', 'dbplyr'))"

ENV SHINY_PATH /srv/shiny-server
RUN rm -rf ${SHINY_PATH}/*
RUN cd /tmp && \
  curl -sOL https://github.com/rstudio/shiny-examples/archive/master.zip && \
  unzip master.zip
RUN cp -r /tmp/shiny-examples-master/051-movie-explorer/* ${SHINY_PATH}
RUN rm -rf /tmp/*

CMD ["/usr/bin/shiny-server.sh"]
