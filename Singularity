Bootstrap: docker
From: debian:jessie-slim

#Includes idba, trimmomatic, samtools, bwa, bedtools, freebayes, bbmap, vcftools, htslib, ncurses, kraken2, resistomeanalyzer, rarefactionanalyzer, SNPfinder

%environment
    export LC_ALL=C

%post
    apt update \
    && apt install -y --no-install-recommends \
    build-essential ca-certificates sudo tcsh\
    git make automake autoconf openjdk-7-jre wget gzip unzip sed\
    zlib1g-dev curl libbz2-dev locales libncurses5-dev liblzma-dev libcurl4-openssl-dev software-properties-common apt-transport-https\
    python3-pip python3-docopt python3-pytest python-dev python3-dev\
    libcurl4-openssl-dev libssl-dev zlib1g-dev fonts-texgyre \
    gcc g++ gfortran libblas-dev liblapack-dev dos2unix\
    r-base-core r-recommended hmmer\
    && rm -rf /var/lib/apt/lists/*

    # Not my favorite workaround, but to get cfsan snp to work with samtools, we have to change which libncurses library is used. Problem is anaconda doesn't have the right version of samtools.
    sudo ln -s /lib/x86_64-linux-gnu/libncursesw.so.5  /lib/x86_64-linux-gnu/libncursesw.so.6

    #Installing Anaconda 2 and Conda 4.5.11
    wget -c https://repo.continuum.io/archive/Anaconda2-5.3.0-Linux-x86_64.sh
    sh Anaconda2-5.3.0-Linux-x86_64.sh -bfp /usr/local

    # add bioconda channels
    conda config --add channels defaults
    conda config --add channels conda-forge
    conda config --add channels bioconda
    # channel for java v8
    conda config --add channels cyclus
    # channel for Lyveset
    conda config --add channels hcc
    

    # install bulk of bioinformatic tools using conda
    conda install zsh java-jdk lyve-set
    # snp-pipeline smalt picard varscan tabix bcftools bowtie2 bwa gatk libdeflate samtools 
    
    ## Workaround to get 3.8 version of GenomeAnalysisTK.jar
    git clone https://github.com/EnriqueDoster/sing_biotools.git
    mv sing_biotools/bin/GenomeAnalysisTK.jar /usr/local/bin/GenomeAnalysisTK.jar
    
    #ln -s /usr/local/envs/snp-tools/bin/* /usr/local/bin/
    
    #Still experimenting with how to change $PATH location. Need to remove GATK jar file to work with cfsan snp
    #echo 'export PATH=$PATH:/usr/local/envs/snp-tools/bin/' >> $SINGULARITY_ENVIRONMENT
    echo 'export CLASSPATH=/usr/local/share/varscan-2.4.4-0/VarScan.jar:$CLASSPATH' >> $SINGULARITY_ENVIRONMENT
    echo 'export CLASSPATH=/usr/local/share/picard-2.21.4-0/picard.jar:$CLASSPATH' >> $SINGULARITY_ENVIRONMENT
    echo 'export CLASSPATH=/usr/local/bin/GenomeAnalysisTK.jar:$CLASSPATH' >> $SINGULARITY_ENVIRONMENT

    # Make sure all the tools have the right permissions to use the tools
    chmod -R 777 /usr/local/

    # install perl modules
    perl -MCPAN -e shell
    install File::Slurp
    install URI::Escape
    install CPAN
    install Sgtty
    install Term::ReadKey
    exit


    
%test
    #which bwa
    #which bedtools
    #which samtools
    #which freebayes
