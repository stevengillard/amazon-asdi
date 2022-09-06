FROM quay.io/condaforge/miniforge3

RUN wget -O /usr/local/bin/dumb-init https://github.com/Yelp/dumb-init/releases/download/v1.2.5/dumb-init_1.2.5_x86_64
RUN chmod +x /usr/local/bin/dumb-init

RUN conda install --yes \
    -c conda-forge \
    python==3.10.4 \
    python-blosc==1.10.6 \
    dask==2022.9.0 \
    distributed==2022.9.0 \
    kerchunk==0.0.7 \
    ujson==5.4.0 \
    lz4==4.0.0 \
    nomkl==1.0 \
    msgpack-python==1.0.4 \
    netcdf4==1.6.0 \
    numpy==1.23.2 \
    pandas==1.4.4 \
    xarray==2022.6.0 \
    bokeh==2.4.3 \
    s3fs==2022.8.2 \
    fsspec==2022.8.2 \
    h5netcdf==1.0.2 \
    tornado==6.2 \ 
    cloudpickle==2.1.0 \
    h5py==3.7.0 \
    zarr==2.12.0 \
    rechunker==0.5.0 \
    intake-esm==2021.8.17 \
    intake==0.6.6 \
    && find /opt/conda/ -type f,l -name '*.a' -delete \
    && find /opt/conda/ -type f,l -name '*.pyc' -delete \
    && find /opt/conda/ -type f,l -name '*.js.map' -delete \
    && find /opt/conda/lib/python*/site-packages/bokeh/server/static -type f,l -name '*.js' -not -name '*.min.js' -delete \
    && rm -rf /opt/conda/pkgs

COPY prepare.sh /usr/bin/prepare.sh
RUN chmod +x /usr/bin/prepare.sh

RUN mkdir /opt/app /etc/dask
COPY dask.yaml /etc/dask/

ENTRYPOINT ["/usr/local/bin/dumb-init", "/usr/bin/prepare.sh"]
