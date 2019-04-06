Bootstrap: docker
From: debian:jessie-slim

#Includes rgi idba trimmomatic bwa samtools bedtools freebayes bbmap vcftools htslib resistomeanalyzer, rarefactionanalyzer, SNPfinder

%environment
    PATH="/usr/local/bin/anaconda/bin:$PATH"
    . activate compute

%post
    ## Jave install doesn't work, but can load java module from summit
    apt update \
    && apt install -y --no-install-recommends \
    build-essential ca-certificates sudo \
    git make automake autoconf wget unzip sed \
    zlib1g-dev curl libbz2-dev locales libncurses5-dev liblzma-dev libcurl4-openssl-dev software-properties-common apt-transport-https\
    libglib2.0-0 libxext6 libsm6 libxrender1 \
    python3-pip python3-docopt python3-pytest python-dev python3-dev\
    libssl-dev zlib1g-dev fonts-texgyre \
    gcc g++ gfortran libblas-dev liblapack-dev dos2unix tabix \
    r-base-core r-recommended hmmer\
    && rm -rf /var/lib/apt/lists/*

    # install anaconda
    if [ ! -d /usr/local/anaconda ]; then
         wget https://repo.continuum.io/miniconda/Miniconda2-4.3.14-Linux-x86_64.sh \
            -O ~/anaconda.sh && \
         bash ~/anaconda.sh -b -p /usr/local/bin/anaconda && \
         rm ~/anaconda.sh
    fi
    # set anaconda path
    export PATH="/usr/local/bin/anaconda/bin:$PATH"

    # install bulk of bioinformatic tools using conda 
    conda create -n compute python=3
    conda install -c bioconda rgi
    
    #conda install numpy scipy
    conda clean --tarballs

    # make /data and /scripts so we can mount it to access external resources
    if [ ! -d /data ]; then mkdir /data; fi
    if [ ! -d /scripts ]; then mkdir /scripts; fi


    
    
%runscript
    echo "Now inside Singularity container woah..."
    exec /bin/bash    
   
%test
