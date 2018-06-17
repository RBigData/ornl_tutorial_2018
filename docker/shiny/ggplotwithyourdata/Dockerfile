FROM rocker/shiny
MAINTAINER "The pbdR Core Team" RBigData@gmail.com
ENV MAKE make -j 4

RUN apt-get update && apt-get install -y --no-install-recommends apt-utils libssl-dev git curl

RUN mkdir -p /R/lib

RUN echo " \
  .libPaths('/R/lib'); \
  options(repos=structure(c(CRAN='https://cran.rstudio.com/'))) ; \
  utils::rc.settings(ipck=TRUE);" > /usr/lib/R/etc/Rprofile.site

RUN rm -rf /usr/lib/R/site-library
RUN rm -rf /usr/local/lib/R/site-library

RUN r -e "install.packages('remotes')"
RUN r -e 'install.packages(c("shiny","shinyjs","ggplot2","scales","DT","tidyr","dplyr","Hmisc","quantreg","markdown","colourpicker","devtools"))'
RUN r -e 'install.packages(c("ggrepel", "plotly"))'

RUN r -e "remotes::install_github('sachsmc/ggkm')"
RUN r -e "remotes::install_github('benjaminrich/table1')"

ENV SHINY_PATH /srv/shiny-server
ENV APP_NAME ggplotwithyourdata
RUN rm -rf ${SHINY_PATH}/*
RUN cd /tmp && \
  curl -sOL https://github.com/smouksassi/${APP_NAME}/archive/master.zip && \
  unzip master.zip
RUN cp -r /tmp/${APP_NAME}-master/shinyapp/* ${SHINY_PATH}
RUN rm -rf /tmp/*

CMD ["/usr/bin/shiny-server.sh"]
