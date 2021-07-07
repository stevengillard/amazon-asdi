FROM quay.io/condaforge/miniforge3

RUN wget -O /usr/local/bin/dumb-init https://github.com/Yelp/dumb-init/releases/download/v1.2.5/dumb-init_1.2.5_x86_64
RUN chmod +x /usr/local/bin/dumb-init

RUN conda install --yes \
    -c conda-forge \
    python==3.8.10 \
    python-blosc==1.10.2 \
    dask==2021.6.2 \
    distributed==2021.6.2 \
    lz4==3.1.3 \
    nomkl==1.0 \
    msgpack-python==1.0.2 \
    netcdf4==1.5.7 \
    numpy==1.21.0 \
    pandas==1.3.0 \
    xarray==0.18.2 \
    bokeh==2.3.2 \
    s3fs==2021.6.1 \
    fsspec==2021.6.1 \
    h5netcdf==0.11.0 \
    tornado==6.1 \ 
    cloudpickle==1.6.0 \
    h5py==3.3.0 \
    zarr==2.8.3 \
    rechunker==0.4.2 \
    && find /opt/conda/ -type f,l -name '*.a' -delete \
    && find /opt/conda/ -type f,l -name '*.pyc' -delete \
    && find /opt/conda/ -type f,l -name '*.js.map' -delete \
    && find /opt/conda/lib/python*/site-packages/bokeh/server/static -type f,l -name '*.js' -not -name '*.min.js' -delete \
    && rm -rf /opt/conda/pkgs

COPY fsspec/*.py /opt/conda/lib/python3.8/site-packages/fsspec/
COPY distributed/*.py /opt/conda/lib/python3.8/site-packages/distributed/

COPY prepare.sh /usr/bin/prepare.sh
RUN chmod +x /usr/bin/prepare.sh

RUN mkdir /opt/app /etc/dask
COPY dask.yaml /etc/dask/

ENTRYPOINT ["/usr/local/bin/dumb-init", "/usr/bin/prepare.sh"]
