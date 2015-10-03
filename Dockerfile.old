FROM ubuntu:14.04

MAINTAINER psytky03 <psytky03@gmail.com>

USER root
ENV bs /birdsuite

RUN apt-get update 
RUN sudo apt-get -y install wget \
python \
build-essential \
make \
gcc \
openjdk-6-jre \
r-base-core \
r-base-dev \
python-numpy \ 
python-setuptools \
bc \
libxp6

RUN mkdir $bs
RUN wget http://www.broadinstitute.org/ftp/pub/mpg/birdsuite/birdsuite_executables_1.5.5.tgz \
&&tar -zxvf birdsuite_executables_1.5.5.tgz -C $bs


WORKDIR $bs

RUN sudo python install.py -e /usr/bin/easy_install 

RUN sudo easy_install birdsuite-1.0-py2.5.egg ; exit 0
RUN sudo easy_install mpgutils-0.7-py2.5.egg ; exit 0

RUN sudo ln -s /usr/local/bin/* . 


RUN wget --no-check-certificate https://cran.r-project.org/src/contrib/mclust_5.0.2.tar.gz
RUN sudo R CMD INSTALL mclust_5.0.2.tar.gz 

RUN tar xvfz broadgap.utils_1.0.tar.gz \
&& cd broadgap.utils \
&& rm -r man \
&& cd .. \
&& R CMD build broadgap.utils


RUN tar -xvf broadgap.cnputils_1.0.tar.gz \
&& cd broadgap.cnputils/ \
&& echo 'exportPattern( "." )' > NAMESPACE \
&& cd .. \
&& R CMD build broadgap.cnputils


RUN tar -xvf broadgap.canary_1.0.tar.gz \
&& cd broadgap.canary/ \
&& echo 'exportPattern( "." )' > NAMESPACE \
&& cd .. \
&& R CMD build broadgap.canary


RUN R CMD INSTALL -l $bs  broadgap.utils_1.0.tar.gz
RUN R CMD INSTALL -l $bs  broadgap.cnputils_1.0.tar.gz 
RUN R CMD INSTALL -l $bs  broadgap.canary_1.0.tar.gz


RUN rm birdsuite.sh \
&& rm run_birdseye.sh

COPY addon/*.* $bs/

RUN chmod 755 MCRInstaller.75.glnxa64.bin \
apt-probeset-summarize.64 \
birdsuite.sh \
run_birdseye.sh


RUN ./MCRInstaller.75.glnxa64.bin -P bean421.installLocation="/birdsuite/MCR75_glnxa64" -silent

COPY METADATADIR.tar.gz $bs/
RUN tar -zxvf METADATADIR.tar.gz 

RUN rm METADATADIR.tar.gz


COPY birdsuite_inputs_1.5.5.tgz /
WORKDIR /

RUN mkdir test_data
RUN tar -zxvf birdsuite_inputs_1.5.5.tgz -C test_data
RUN rm birdsuite_inputs_1.5.5.tgz
RUN rm birdsuite_executables_1.5.5.tgz

