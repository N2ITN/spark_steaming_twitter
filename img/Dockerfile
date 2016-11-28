FROM phusion/baseimage
RUN apt-get update
RUN apt-get -y install apt-utils
RUN apt-get upgrade -y
RUN apt-get install wget
# RUN apt-get install sudo
WORKDIR ~/
COPY . ./
RUN wget http://repo.continuum.io/miniconda/Miniconda3-3.7.0-Linux-x86_64.sh -O miniconda.sh
RUN apt-get install bzip2
RUN bash miniconda.sh -b -p miniconda
RUN export PATH="$HOME/miniconda/bin:$PATH"
ENV PATH $HOME/miniconda/bin:$PATH
RUN apt-get install git -y
RUN git clone git://github.com/apache/spark.git -b branch-2.0
RUN ls
# RUN conda install jupyter
# CMD ["jupyter", "notebook"]

