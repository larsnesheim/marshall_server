# marshall_server
Information about the Bristol Econometrics server: Marshall

server address:    marshall.efm.bris.ac.uk

# Current users
we23202        Lars Nesheim
               Stefan Hubner


# Unix tips

# set unlimited stack size
ulimit -s unlimited

# build openmpi

wget xf https://download.open-mpi.org/release/open-mpi/v5.0/openmpi-5.0.5.tar.bz2
tar xf openmpi-5.0.5.tar.bz2
cd openmpi-5.0.5
./configure \
    CC=${ONEAPI_ROOT}/compiler/2024.2/bin/icx \
    CXX=${ONEAPI_ROOT}/compiler/2024.2/bin/icpx \
    FC=${ONEAPI_ROOT}/compiler/2024.2/bin/ifx \
    F77=${ONEAPI_ROOT}/compiler/2024.2/bin/ifx \
    OMPI_CC=${ONEAPI_ROOT}/compiler/2024.2/bin/icx \
    OMPI_CXX=${ONEAPI_ROOT}/compiler/2024.2/bin/icpx \
    OMPI_FC=${ONEAPI_ROOT}/compiler/2024.2/bin/ifx \
    OMPI_F77=${ONEAPI_ROOT}/compiler/2024.2/bin/ifx \
    --prefix=/opt/openmpi-5.0.5
sudo make install -j 32 
export PATH=/opt/openmpi-5.0.5/bin:$PATH
export LD_LIBRARY_PATH=/opt/optenmpi-5.0.5/lib:$LD_LIBRARY_PATH
