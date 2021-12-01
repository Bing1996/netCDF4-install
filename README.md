# **netCDF4.5.0 Installnation**
## 1.**Describtion**
This project allows users to install netCDF4.5.0 automaticly, this version only supports netCDF4.5.0 installnation. Firstly, the various files included are introduced in the next part. In the third section, a detailed install introduction is attached, and some errors encountered is demenstrated in the last sections. 

## 2.**What files in this project**
### six essential .tar.gz files:
* zlib-1.2.11.tar.gz
* hdf5-1.10.3.tar.gz
* curl-7.57.0.tar.gz
* v4.5.0.c.tar.gz (netcdf-C)
* v4.4.0.fortran.tar.gz(netcdf-fortran)
* v4.3.0.tar.gz(netcdf-c++)
### install bash:
* install.sh
### other files:
* LISENCE
* README.md
## 3.**How to install**
### automatic install

* **install.sh**
    ```shell
    git clone https://github.com/Bing1996/netCDF4-install.git
    cd netCDF4-install.git
    sudo bash install.sh
    ```
### manual install

This section for users who want to install seprately. Three libraries rquired and netCDF4-C and netCDF4-Fortran mentioned in the section 2 will be installed.

*Note:netCDF4-Fortran cannot be installed until netCDF4-C has been installed and compiled successfully!*

* **zlib-1.2.11**
    ```shell
    tar -zxvf zlib-1.2.11.tar.gz
    cd zlib-1.2.11
    ZDIR=/usr/local/
    sudo ./configure --prefix=${ZDIR}
    sudo make check             # check environment
    sudo make isntall
    ```
* **curl-7.57.0**  
    ```shell
    tar -zxvf curl-7.57.0.tar.gz
    cd curl-7.57.0
    CURLDIR=/usr/local/
    sudo ./configure --prefix=${CURLDIR}
    sudo make check             
    sudo make isntall
    ```
* **hdf5-1.10.3**
    ```shell
    tar -zxvf hdf5-1.10.3tar.gz
    cd hdf5-1.10.3
    H5DIR=/usr/local/
    sudo ./configure --with-zlib=${ZDIR} --prefix=${H5DIR}
    sudo make check             
    sudo make isntall
    ```
* **netCDF4**
    ```shell
    tar -zxvf v4.5.0.tar.gz
    cd netcdf-c-4.5.0
    NCDIR=/usr/local/
    sudo CPPFLAGS=-I${H5DIR}/include LDFLAGS=-L${H5DIR}/lib \
    ./configure --prefix=${NCDIR}
    sudo make check             
    sudo make isntall
    ```
* **netCDF4-fortran**

    First make sure the netCDF C library has been built, tested, and installed. The shell variable NCDIR should be set such that the shared library for netCDF C is under \${NCDIR}/lib and netCDF utilities such as ncdump are under \${NCDIR}/bin.
    ```shell
    tar -zxvf v4.4.0.tar.gz
    cd netcdf-fortran-4.4.0
    NFDIR=/usr/local/
    CPPFLAGS=-I${NCDIR}/include LDFLAGS=-L${NCDIR}/lib \
    ./configure --prefix=${NFDIR}
    sudo make check             
    sudo make isntall
    ```
    If the netCDF C library was installed as a shared library in a location that is not searched by default, you will need to set the LD_LIBRARY_PATH environment variable (or DYLD_LIBRARY_PATH on OSX) to specify that directory before running the configure script.
    ```shell
    export LD_LIBRARY_PATH=${NCDIR}/lib:${LD_LIBRARY_PATH}
    ```

* **netCDF4-cxx4**

    Lynton Appel, of the Culham Centre for Fusion Energy (CCFE) in Oxfordshire,
    has developed and contributed a netCDF-4 C++ library that depends on an 
    installed netCDF-4 C library. The netCDF-4 C++ API was developed for use 
    in managing fusion research data from CCFE's innovative MAST (Mega Amp 
    Spherical Tokamak) experiment.

    ```shell
    tar -zxvf 4.3.0.tar.gz
    cd netcdf-cxx4-4.3.0
    mkdir build
    cd build
    ../configure
    make
    sudo make check
    sudo make install
    ```

## 4.**Some error encounter**
* *Missing c++ enssential library while installing hdf5 lib*    
    ```shell
    sudo apt install build-essential
    sudo apt install g++
    ```   
* *Missing m4 library while installing netCDF4-C lib*
    ```
    sudo apt install m4
    ```
* *Undefined __netCDF__MOD_nf_open()*
    ```shell
    export LD_LIBRARY_PATH=${NCDIR}/lib:${LD_LIBRARY_PATH}
    ```
    before running the Fortran script, for example:
    ```shell
    gfortran -I /usr/local/include targetFortranFile.f90 -L /usr/local/lib -lnetcdff -lnetcdf -lnetcdf
    ```

    