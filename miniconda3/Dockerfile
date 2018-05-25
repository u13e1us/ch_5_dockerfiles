FROM debian

LABEL maintainer=@joshuacook
ARG DEBIAN_FRONTEND=noninteractive
#RUN apt-get update --fix-missing && \
#	apt-get install -y \
#	wget bzip2 ca-certificates \
#	libglib2.0-0 libxext6 libsm6 libxrender1


#RUN echo 'export PATH=/opt/conda/bin:$PATH' > /etc/profile.d/conda.sh && \



#RUN apt-get update 

#RUN	apt-get install -y wget

#RUN	echo 'export PATH=/opt/conda/bin:$PATH' > /etc/profile.d/conda.sh && \
#	wget --quiet  \ 
#	https://repo.continuum.io/miniconda/Miniconda3-4.3.11-Linux-x86_64.sh \ 	--output-file=~/miniconda.sh && \
#	/bin/bash ~/miniconda.sh -b -p /opt/conda && \
#	rm ~/miniconda.sh 

ENV LANG=C.UTF-8 LC_ALL=C.UTF-8
ENV PATH /opt/conda/bin:$PATH

RUN apt-get update --fix-missing && \
    apt-get install -y wget bzip2 ca-certificates curl git && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN wget --quiet https://repo.continuum.io/miniconda/Miniconda3-4.4.10-Linux-x86_64.sh -O ~/miniconda.sh && \
    /bin/bash ~/miniconda.sh -b -p /opt/conda && \
    rm ~/miniconda.sh && \
    /opt/conda/bin/conda clean -tipsy && \
    ln -s /opt/conda/etc/profile.d/conda.sh /etc/profile.d/conda.sh && \
    echo ". /opt/conda/etc/profile.d/conda.sh" >> ~/.bashrc && \
echo "conda activate base" >> ~/.bashrc


RUN apt-get install -y curl grep sed dpkg && \
	TINI_VERSION=`curl https://github.com/krallin/tini/releases/latest | grep -o "/v.*\"" | sed 's:^..\(.*\).$:\1:'` && \
	curl -L "https://github.com/krallin/tini/releases/download/v${TINI_VERSION}/tini_${TINI_VERSION}.deb" > tini.deb && \
	dpkg -i tini.deb && \
	rm tini.deb && \
	apt-get clean




ENV LANG=C.UTF-8 LC_ALL=C.UTF-8
ENV PATH /opt/conda/bin:$PATH

ENTRYPOINT [ "/usr/bin/tini", "--" ]
