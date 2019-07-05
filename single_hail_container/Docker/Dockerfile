#=========================#
#  Operating System setup #
#=========================#
from centos:centos7

# install basic build environment
RUN yum -y install epel-release && yum -y update && \
    yum -y install gcc g++ gcc-gfortran zlib-devel libxml2-devel && \
    yum -y install libcurl-devel make netcdf-devel libpng-devel && \
    yum -y install python libconfig-devel bc udunits2-devel && \
    yum -y install gsl-devel lapack-devel hdf5-devel compat-libf2c-34 && \
    rm -rf /var/lib/apt/lists/*


#install hydroclass binaries in /opt/hydroclass
COPY hca.tar /opt
RUN mkdir /opt/hydroclass && \
    tar -xf /opt/hca.tar -C /opt/hydroclass && \
    rm -rf /opt/hca.tar
ENV PATH=/opt/hydroclass:$PATH

#install necessary libraries for hydroclass 
COPY hc_lib.tar /opt
RUN tar -xf /opt/hc_lib.tar && \
    rm -rf /opt/hc_lib.tar
ENV LD_LIBRARY_PATH=/opt/hc_lib:$LD_LIBRARY_PATH

