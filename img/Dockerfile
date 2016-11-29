FROM phusion/baseimage
RUN apt-get update
RUN apt-get -y install apt-utils
RUN apt-get upgrade -y
RUN apt-get install wget
# RUN apt-get install sudo

RUN wget http://repo.continuum.io/miniconda/Miniconda3-3.7.0-Linux-x86_64.sh -O miniconda.sh
RUN apt-get install bzip2
RUN bash miniconda.sh -b -p miniconda
RUN apt-get install git -y
RUN git clone git://github.com/apache/spark.git -b branch-2.0
RUN apt-get install tree -y
ENV PATH /miniconda/bin:$PATH
RUN conda install --yes jupyter
# RUN apt-get install python-pip -y
# RUN pip install notebook
RUN tree -d -L 2
RUN ls
# Add Tini. Tini operates as a process subreaper for jupyter. This prevents
# kernel crashes.
ENV TINI_VERSION v0.6.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /usr/bin/tini
RUN chmod +x /usr/bin/tini
RUN conda install --yes pip
RUN pip install tweepy 

RUN conda install --yes -c conda-forge py4j=0.10.3 
# ENV PATH usr/bin/python3:$PATH
ENV SPARK_HOME /spark
ENV PYTHONPATH $SPARK_HOME/python:$SPARK_HOME/python/build:$PYTHONPATH 
ENTRYPOINT ["/usr/bin/tini", "--"]
# WORKDIR ~/
RUN conda update nb_conda nb_conda_kernels 
RUN add-apt-repository ppa:webupd8team/java
RUN apt-get update


RUN apt-get install -y software-properties-common

RUN echo "oracle-java8-installer shared/accepted-oracle-license-v1-1 select true" | debconf-set-selections
RUN echo "oracle-java8-installer shared/accepted-oracle-license-v1-1 seen true" | debconf-set-selections

RUN apt-get install -y oracle-java8-installer
ENV PYSPARK_SUBMIT_ARGS "--master local[2] pyspark-shell"
ENV SPARK_LOCAL_IP 127.0.0.1

COPY . ./

EXPOSE 8888
CMD ["jupyter", "notebook", "--port=8888", "--no-browser", "--ip=0.0.0.0"]


# docker run -it -p 666:8888 docker-whale /bin/bash
# docker build -t docker-whale .
# docker run -p 666:8888 docker-whale

# jupyter notebook --port=8888 --no-browser --ip=0.0.0.0  --MappingKernelManager.default_kernel_name=Python[conda-root]