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
    zlib1g-dev curl libbz2-dev locales libncurses5-dev liblzma-dev libcurl4-openssl-dev software-properties-common apt-transport-https\
    python3-pip python3-docopt python3-pytest python-dev python3-dev\
    libcurl4-openssl-dev libssl-dev zlib1g-dev fonts-texgyre \
    gcc g++ gfortran libblas-dev liblapack-dev dos2unix tabix \
    && rm -rf /var/lib/apt/lists/*

    # Anaconda
    cd /usr/local/
    wget https://repo.continuum.io/archive/Anaconda3-2018.12-Linux-x86_64.sh
    bash Anaconda3-2018.12-Linux-x86_64.sh -b -p /opt/anaconda3
    rm Anaconda3-2018.12-Linux-x86_64.sh
    #. /opt/anaconda3/etc/profile.d/conda.sh
    #conda config --set auto_update_conda False
    #conda install -y -n base conda=4.5.11 
    #conda create -n base -f /environment-stable.yml
    echo 'export PATH=$PATH:/opt/anaconda3/bin/' >>$SINGULARITY_ENVIRONMENT
    /opt/anaconda3/bin/conda create -n com_tools python=2.7 anaconda
    . /opt/anaconda3/bin/activate com_tools 
    /opt/anaconda3/bin/conda install sqlite=3.13 tk=8.5 readline=7.0
    /opt/anaconda3/bin/conda install -c conda-forge -c bioconda rgi=4.2.2
    #source activate com_tools
    #sudo ln -s /opt/anaconda3/etc/profile.d/conda.sh /etc/profile.d/conda.sh
    #/opt/anaconda3/bin/conda activate
    #echo "conda activate" >> ~/.bashrc
    #/opt/anaconda3/bin/conda activate com_tools
    #/opt/anaconda3/bin/conda install -c bioconda rgi
    
   
%test
