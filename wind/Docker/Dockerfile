#=========================#
#  Operating System setup #
#=========================#
from ubuntu:18.04

# install basic build environment
RUN apt-get update && \
    apt-get -y install apt-utils && \
    apt-get -y upgrade && \
    apt-get -y install gcc g++ zlib1g-dev libxml2-dev && \
    apt-get -y install curl make libnetcdf-dev libpng-dev && \
    apt-get -y install python libconfig-dev bc && \
    apt-get -y install exim4 exim4-config && \
    rm -rf /var/lib/apt/lists/*

# install mvtGENI software stack without ldm
# install libconfig in /opt/libconfig
COPY libconfig-1.5.tar.gz /opt
RUN mkdir /opt/libconfig && \
    tar xzf /opt/libconfig-1.5.tar.gz -C /opt/libconfig && \
    cd /opt/libconfig/libconfig-1.5 && \
    ./configure --prefix=/usr/local/libconfig && \
    make && make install && \
    cd /opt && \
    rm -rf /opt/libconfig && \
    rm /opt/libconfig-1.5.tar.gz
ENV LD_LIBRARY_PATH=/usr/local/libconfig/lib:$LD_LIBRARY_PATH

# install jansson in /opt/jansson
COPY jansson-2.7.tar.gz /opt
RUN mkdir /opt/jansson && \
    tar xzf /opt/jansson-2.7.tar.gz -C /opt/jansson && \
    cd /opt/jansson/jansson-2.7 && \
    ./configure --prefix=/usr/local/jansson && \
    make && make install && \
    cd /opt && \
    rm -rf /opt/jansson && \
    rm /opt/jansson-2.7.tar.gz
ENV LD_LIBRARY_PATH=/usr/local/jansson/lib:$LD_LIBRARY_PATH

# install mvt
COPY mvt.tar /opt
RUN tar xf /opt/mvt.tar -C /opt && \
    cd /opt/mvt && make && \
    cd /opt && rm /opt/mvt.tar
ENV MVTHOME=/opt/mvt
ENV PATH=/opt/mvt:$PATH

# install UM_VEL
COPY UM_VEL.tar /opt
RUN tar xf /opt/UM_VEL.tar -C /opt && \
    cd /opt/UM_VEL && make && \
    cd /opt && rm /opt/UM_VEL.tar
ENV UM_VEL=/opt/UM_VEL
ENV PATH=/opt/UM_VEL:$PATH

# install netcdf2png
COPY netcdf2png.tar /opt
RUN tar xf /opt/netcdf2png.tar -C /opt && \
    cd /opt/netcdf2png && make && \
    cd /opt && rm /opt/netcdf2png.tar
ENV PATH=/opt/netcdf2png:$PATH

# install pointAlert
COPY pointAlert.tar /opt
RUN tar xf /opt/pointAlert.tar -C /opt && \
    cd /opt/pointAlert && make && \
    cd /opt && rm /opt/pointAlert.tar
ENV POINT_ALERT_HOME=/opt/pointAlert
ENV PATH=/opt/pointAlert:$PATH

# email notification
#COPY email_notification.tar /opt
#RUN tar xf /opt/email_notification.tar -C /opt && \
#    cd /opt/email_notification && make && \
#    cd /opt && rm email_notification.tar

#ENV EMAIL_NOTIFICATION_HOME=/opt/email_notification
#ENV PATH=/opt/email_notification/email_notification:$PATH

#COPY update-exim4.conf.conf /etc/exim4
#RUN update-exim4.conf
