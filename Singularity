Bootstrap: docker
From: debian:jessie-slim

#Includes idba, trimmomatic, samtools, bwa, bedtools, freebayes, bbmap, resistomeanalyzer, rarefactionanalyzer

%environment
    #. /opt/anaconda3/bin/activate com_tools

%post
    ## Jave install doesn't work, but can load java module from server
    
    ## Install basic functions, compilers, and dev tools
    apt update \
    && apt install -y --no-install-recommends \
    build-essential ca-certificates sudo \
    git make automake autoconf openjdk-7-jre wget unzip sed \
    pkg-config libfreetype6-dev libpng12-dev ncbi-blast+ prodigal\
    zlib1g-dev curl libbz2-dev locales libncurses5-dev liblzma-dev libcurl4-openssl-dev software-properties-common apt-transport-https\
    python3-pip python3-docopt python3-pytest python-dev python3-dev\
    libcurl4-openssl-dev libssl-dev zlib1g-dev fonts-texgyre \
    gcc g++ gfortran libblas-dev liblapack-dev dos2unix tabix \
    && rm -rf /var/lib/apt/lists/*

    python3 -m pip install biopython
    python3 -m pip install six
    python3 -m pip install filetype
    python3 -m pip install pytest
    python3 -m pip install mock
    python3 -m pip install pandas
    python3 -m pip install matplotlib==2.2.3
    python3 -m pip install seaborn
    python3 -m pip install pyfaidx
    python3 -m pip install pyahocorasick
    
    
    cd /usr/local/
    wget http://github.com/bbuchfink/diamond/releases/download/v0.8.36/diamond-linux64.tar.gz && \
    tar xvf diamond-linux64.tar.gz && \
    mv diamond /usr/local/bin
    
    
    cd /usr/local/
    git clone https://github.com/arpcard/rgi.git
    cd rgi/
    python3 -m pip install -r requirements.txt
    python3 -m pip install .
    
   
%test
