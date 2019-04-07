Bootstrap: docker
From: debian:jessie-slim

#Includes rgi idba trimmomatic bwa samtools bedtools freebayes bbmap vcftools htslib resistomeanalyzer, rarefactionanalyzer, SNPfinder

%environment
    echo 'export PATH=c/usr/local/bin/anaconda/bin:${PATH}' >> $SINGULARITY_ENVIRONMENT
    
%post
    ## Jave install doesn't work, but can load java module from summit
    apt update \
    && apt install -y --no-install-recommends \
    build-essential ca-certificates sudo \
    git make automake autoconf wget unzip sed \
    zlib1g-dev curl libbz2-dev locales libncurses5-dev liblzma-dev libcurl4-openssl-dev software-properties-common apt-transport-https\
    libglib2.0-0 libxext6 libsm6 libxrender1 \
    python3.6 python3-pip python3-docopt python3-pytest python-dev python3-dev\
    libssl-dev zlib1g-dev fonts-texgyre \
    gcc g++ gfortran libblas-dev liblapack-dev dos2unix tabix \
    r-base-core r-recommended hmmer\
    && rm -rf /var/lib/apt/lists/*

    python3 -m pip install six
    python3 -m pip install biopython
    python3 -m pip install filetype
    python3 -m pip install pytest
    python3 -m pip install mock
    python3 -m pip install pandas
    python3 -m pip install matplotlib
    python3 -m pip install seaborn
    python3 -m pip install pyfaidx
    python3 -m pip install pyahocorasick
    
    git clone https://github.com/arpcard/rgi.git
    cd rgi
    python3 -m pip install .


%runscript


%test
