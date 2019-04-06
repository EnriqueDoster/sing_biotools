Bootstrap: docker
From: debian:jessie-slim

#Includes rgi idba trimmomatic bwa samtools bedtools freebayes bbmap vcftools htslib resistomeanalyzer, rarefactionanalyzer, SNPfinder

%environment
    #PATH="/usr/local/bin/anaconda/bin:$PATH"

    #source /usr/local/bin/anaconda/bin/activate compute

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
    if [ ! -d /usr/local/bin/anaconda ]; then
         wget https://repo.continuum.io/archive/Anaconda3-2019.03-MacOSX-x86_64.sh \
            -O /usr/local/anaconda.sh && \
         bash /usr/local/anaconda.sh -b -p /usr/local/bin/anaconda && \
         rm /usr/local/anaconda.sh
    fi
    
    # add bioconda channels
    conda config --add channels defaults
    conda config --add channels conda-forge
    conda config --add channels bioconda
    conda update conda
    conda clean --all --yes
    
    # set anaconda path
    #export PATH="/usr/local/bin/anaconda/bin:$PATH"
    # install bulk of bioinformatic tools using conda 
    conda create -n compute python=3 rgi
    
    #conda install numpy scipy
    conda clean --tarballs

    # make /data and /scripts so we can mount it to access external resources
    if [ ! -d /data ]; then mkdir /data; fi
    if [ ! -d /scripts ]; then mkdir /scripts; fi


    
    
%runscript


%test
