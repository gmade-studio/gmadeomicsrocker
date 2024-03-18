FROM rocker/verse:4.2.3
MAINTAINER "Yanhua Zheng" zyh3084989256@gmail.com

RUN apt-get update \
  && apt-get install -y --no-install-recommends \
    libnetcdf-dev \
    ## rgl support
    libgl1-mesa-dev \
    libglu1-mesa-dev \
    ## tcl tk support
    tcl8.6-dev \
    tk8.6-dev \
    ## python-env && pip3 support
    python3.10-venv \
    python3-pip
RUN install2.r --error \
     pak 
RUN R -e "pak::pkg_install(c('xcms','WGCNA', 'KEGGREST', 'KEGGgraph', 'plotly','pROC','sva','limma'),upgrade = TRUE,ask= FALSE, dependencies = NA)" 
RUN R -e "pak::pkg_install(c('fs','keras','tensorflow','pins','flextable','torch','mlr3verse','R6','reticulate', 'GSVA'),upgrade = TRUE,ask= FALSE, dependencies = NA)" 
RUN R -e "pak::pkg_install(c('graphite','clusterProfiler','igraph','ggraph'),upgrade = TRUE,ask= FALSE, dependencies = NA)"
RUN R -e "pak::pkg_install(c('rstudio/tfhub','rstudio/tfdatasets','yufree/enviGCMS','yufree/pmd','yufree/mzrtsim','yufree/rmwf','mlr-org/mlr3proba','mlr-org/mlr3extralearners@*release'),upgrade = TRUE,ask= FALSE, dependencies = NA)"
RUN rm -rf /tmp/downloaded_packages 
RUN R -e "pak::cache_clean()"
RUN strip /usr/local/lib/R/site-library/*/libs/*.so 
WORKDIR /usr/src/app
RUN python3 -m pip install --no-cache-dir --upgrade pip && \
    python3 -m pip install --no-cache-dir \ 
    tensorflow==2.11.* \
    tensorflow-hub \
    tensorflow-datasets \
    scipy \
    protobuf \
    requests \
    Pillow \
    h5py \
    pandas \
    pydot \
    torch_geometric \
    pqi \
    mygene \
    configparser \
    numpy \
    scikit-learn \
    tqdm \
    lifelines \
    matplotlib \
    captum \
    scipy 
RUN python3 -m pip install --no-cache-dir torch  torchvision torchaudio  --index-url https://download.pytorch.org/whl/cpu 
RUN python3 -m pip install --no-cache-dir pyg_lib torch_scatter torch_sparse torch_cluster  torch_spline_conv  -f https://data.pyg.org/whl/torch-2.0.0+cpu.html 
COPY . .