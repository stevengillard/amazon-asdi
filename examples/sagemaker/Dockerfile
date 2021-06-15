FROM quay.io/condaforge/miniforge3

ARG NB_USER="sagemaker-user"
ARG NB_UID="1000"
ARG NB_GID="100"

RUN apt-get update && \
    apt-get install -y git sudo && \
    useradd -m -s /bin/bash -N -u $NB_UID $NB_USER && \
    chmod g+w /etc/passwd && \
    echo "${NB_USER}    ALL=(ALL)   NOPASSWD:   ALL" >> /etc/sudoers && \
    rm -rf /var/lib/apt/lists/*
    
RUN conda install --yes \
    -c conda-forge \
    python==3.8.10 \
    boto3 \
    ipykernel \
    ipywidgets \
    basemap \
    proj \
    python-blosc==1.10.2 \
    dask==2021.6.0 \
    lz4==3.1.3 \
    nomkl==1.0 \
    msgpack-python==1.0.2 \
    netcdf4==1.5.6 \
    numpy==1.20.3 \
    pandas==1.2.4 \
    xarray==0.18.2 \
    bokeh==2.3.2 \
    s3fs==2021.5.0 \
    fsspec==2021.5.0 \
    h5netcdf==0.11.0 \
    distributed==2021.6.0 \
    tornado==6.1 \ 
    cloudpickle==1.6.0 \
    h5py==3.1.0 \
    zarr==2.8.1 \
    rechunker==0.4.2 \
    && find /opt/conda/ -type f,l -name '*.a' -delete \
    && find /opt/conda/ -type f,l -name '*.pyc' -delete \
    && find /opt/conda/ -type f,l -name '*.js.map' -delete \
    && find /opt/conda/lib/python*/site-packages/bokeh/server/static -type f,l -name '*.js' -not -name '*.min.js' -delete \
    && rm -rf /opt/conda/pkgs
    
RUN python3 -m ipykernel install --sys-prefix
    
ENV SHELL=/bin/bash
USER $NB_UID

