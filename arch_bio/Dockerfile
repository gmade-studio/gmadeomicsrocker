FROM danysk/docker-manjaro-linux-with-yay:latest
RUN yay -Syu --noconfirm &&\
    yay -S --noconfirm snakemake &&\
    yay -S --noconfirm r &&\
    #pacman -S python-pulp --noconfirm &&\
    yay -S --noconfirm snakemake &&\
    yay -S --noconfirm miniconda3 &&\
    yay -S --noconfirm fastqc &&\
    yay -S --noconfirm samtools &&\
    yay -S --noconfirm trim_galore &&\
    yay -S --noconfirm cutadapt &&\
    yay -S --noconfirm sambamba &&\
    yay -S --noconfirm htslib &&\
    yay -S --noconfirm tabix &&\
    yay -S --noconfirm seqkit &&\
    yay -S --noconfirm bedtools &&\
    #yay -S --noconfirm rstudio-server-git &&\
    # wgbstools 设置环境变量
    pacman -S python-pandas python-numpy python-scipy --noconfirm &&\
    git clone https://github.com/nloyfer/wgbs_tools.git &&\
    cd wgbs_tools &&\
    python setup.py &&\
    cd .. &&\
    git clone https://github.com/nloyfer/UXM_deconv.git &&\
    sudo ln -s /opt/miniconda3/etc/profile.d/conda.sh /etc/profile.d/conda.sh &&\
    echo "[ -f /opt/miniconda3/etc/profile.d/conda.sh ] && source /opt/miniconda3/etc/profile.d/conda.sh" >> ~/.bashrc &&\
    source ~/.bashrc &&\
    export CRYPTOGRAPHY_OPENSSL_NO_LEGACY=1 &&\
    conda config --add channels bioconda &&\
    conda config --add channels conda-forge &&\
    conda config --set channel_priority strict &&\
    conda create -n qualimap -c bioconda qualimap -y &&\
    conda create -n mhaptools -c bioconda mhaptools -y &&\
    conda create -n methyldackel -c bioconda methyldackel -y  &&\
    conda create -n bsmap -c bioconda bsmap -y &&\
    yay -Sc --noconfirm &&\
    conda clean --all &&\
    R -e "install.packages('pak')" &&\ 
    R -e "pak::pkg_install(c('optparse','openxlsx','R6','reticulate', 'GSVA','graphite','igraph','ggraph','TCGAbiolinks','SummarizedExperiment','doParallel','yaml','tinytex','KEGGgraph', 'plotly','pROC','sva','glue','fs','png','reshape2','readxl','sampling','pdftools','umap','gridExtra','ggpubr','GenomicRanges','data.table','clusterProfiler','org.Hs.eg.db','msigdbr','xlsx','KEGGREST','GenomicDataCommons','foreach','doMC','Seurat', 'dbplyr', 'RColorBrewer','rjson','tidyverse','mlr3verse','limma'),upgrade = TRUE,ask= FALSE, dependencies = NA)"  &&\
    R -e "pak::pkg_install(c('mlr-org/mlr3extralearners@*release'),upgrade = TRUE,ask= FALSE, dependencies = NA)" &&\
    R -e "install.packages('mlr3proba', repos = 'https://mlr-org.r-universe.dev')" &&\
    R -e "tinytex::install_tinytex(force = TRUE)" &&\
    R -e "tinytex::tlmgr_repo('http://mirrors.tuna.tsinghua.edu.cn/CTAN/')" &&\
    rm -rf /tmp/downloaded_packages && \
    R -e "pak::cache_clean()" 
ENV PATH=wgbs_tools:$PATH
ENV PATH=UXM_deconv:$PATH
ENV CRYPTOGRAPHY_OPENSSL_NO_LEGACY=1
WORKDIR /home/builduser
EXPOSE 80
EXPOSE 443
EXPOSE 8080
EXPOSE 8787
USER builduser
ENTRYPOINT [ "/bin/bash", "-c", "source /opt/miniconda3/etc/profile.d/conda.sh && conda activate" ]


