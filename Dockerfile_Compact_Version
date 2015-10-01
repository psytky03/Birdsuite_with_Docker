FROM ubuntu:14.04

MAINTAINER psytky03 <psytky03@gmail.com>

USER root
ENV bs /birdsuite

RUN apt-get update && apt-get install -y --no-install-recommends \
wget \
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
libxp6 \
&& apt-get clean \
&& apt-get autoremove 

# Download birdsuite_executable files
RUN mkdir $bs \
&& wget http://www.broadinstitute.org/ftp/pub/mpg/birdsuite/birdsuite_executables_1.5.5.tgz \
&& tar -zxvf birdsuite_executables_1.5.5.tgz -C $bs \
&& rm birdsuite_executables_1.5.5.tgz \
&& rm $bs/birdsuite.sh $bs/run_birdseye.sh


RUN wget https://dl.dropboxusercontent.com/u/964493/additional.tar.gz \
&& tar -zxvf additional.tar.gz \
&& rm additional.tar.gz \
&& mv METADATADIR.tar.gz $bs/ \
&& tar -zxvf $bs/METADATADIR.tar.gz -C $bs \
&& rm $bs/METADATADIR.tar.gz \
&& mv addon/* $bs/ \
&& chmod 755 $bs/MCRInstaller.75.glnxa64.bin \
$bs/apt-probeset-summarize.64 \
$bs/birdsuite.sh \
$bs/run_birdseye.sh \
&& $bs/MCRInstaller.75.glnxa64.bin -P bean421.installLocation="/birdsuite/MCR75_glnxa64" -silent \
&& rm $bs/MCRInstaller.75.glnxa64.bin \
&& mkdir test_data data \
&& tar -zxvf birdsuite_inputs_1.5.5.tgz -C test_data \
&& rm birdsuite_inputs_1.5.5.tgz


# Install Python tools
WORKDIR $bs 

RUN sudo python install.py -e /usr/bin/easy_install 
RUN sudo easy_install birdsuite-1.0-py2.5.egg ; exit 0 
RUN sudo easy_install mpgutils-0.7-py2.5.egg ; exit 0 
RUN sudo ln -s /usr/local/bin/* . \
&& rm *.egg \
&& rm *.py


# Install R packages 
#
RUN wget --no-check-certificate https://cran.r-project.org/src/contrib/mclust_5.0.2.tar.gz \
&& sudo R CMD INSTALL mclust_5.0.2.tar.gz \
&& rm mclust_5.0.2.tar.gz 

RUN tar -xvf broadgap.utils_1.0.tar.gz \
\
# Fix broadgap.utils
&& cd broadgap.utils \
&& rm -r man \
&& cd .. \
&& R CMD build broadgap.utils \
\
# Fix broadgap.cnputils
&& tar -xvf broadgap.cnputils_1.0.tar.gz \
&& cd broadgap.cnputils/ \
&& echo 'exportPattern( "." )' > NAMESPACE \
&& cd .. \
&& R CMD build broadgap.cnputils \
\
# Fix broadgap.canary
&& tar -xvf broadgap.canary_1.0.tar.gz \
&& cd broadgap.canary/ \
&& echo 'exportPattern( "." )' > NAMESPACE \
&& cd .. \
&& R CMD build broadgap.canary \
&& rm -r broadgap.utils broadgap.cnputils broadgap.canary \
&& R CMD INSTALL -l $bs  broadgap.utils_1.0.tar.gz \
&& R CMD INSTALL -l $bs  broadgap.cnputils_1.0.tar.gz \
&& R CMD INSTALL -l $bs  broadgap.canary_1.0.tar.gz \
&& rm -f broadgap.utils_1.0.tar.gz broadgap.cnputils_1.0.tar.gz broadgap.canary_1.0.tar.gz

WORKDIR /
