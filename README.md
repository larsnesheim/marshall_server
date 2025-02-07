# Marshall server
This site contains information about the Bristol Econometrics server: Marshall

server address:    marshall.efm.bris.ac.uk

# Current users
````
1. we23202        Lars Nesheim
2.                Stefan Hubner
````

# Unix tips

# set unlimited stack size
````
ulimit -s unlimited
````
# build openmpi
````
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
````

#disks:
````
  # df -h / /opt /home/
  Filesystem                    Size  Used Avail Use% Mounted on
  /dev/mapper/rl_marshall-root  120G   19G  102G  16% /
  /dev/mapper/rl_marshall-opt   200G   66G  135G  33% /opt
  /dev/mapper/data-home         2.2T   20G  2.2T   1% /home

/home = bulk data space

/opt = software

230GB unallocated. Options: 
     1) add to the swap,
     2) add to root,
     3) add to opt
     4) create /tmp or other

512 SSD. Options:
     1) a separate "fast" area?
     2) Cache for /home
        (not particular resilient SSD in terms of server-level SSD endurance (500TBW endurance total) to cope
          with being a heavy-use cache for the data.)
````

#Questions
1. Backups are not yet enabled
2. "soft" disk quota limits for /home for now at 1000GB


# Software
1.  [X] CUDA
  => 12.6 installed along with GPU drivers for this.
  `nvidia-smi` displays correct info for card and driver.
  No further testing done.

2. [X] gcc and gfortran
  -> Default system versions installed (8.4)
  => gcc 14.2.0 installed from local repo, available via `module` commands

3. [X] R
  => R 4.4.1 installed already by "Compute" role

4. [X] Julia
  => 1.10.4 installed from local repo, available via `module`

5. [X] Matlab R2024
  => Installed from local repo, available via `module`

6. [X] Rstudio (for EL8)
  -> tar.gz for latest version from : https://download1.rstudio.org/electron/rhel8/x86_64/rstudio-2024.09.0-375-x86_64-fedora.tar.gz
  => Installed into /opt/ with a module but not yet tested in a GUI
  => Available via `module`

7. [X] Python
  -> 3.6.8 provided by system packages as `python3`
  -> `python3.11` already installed as well
  -> Note that the 3.6.8 version is the one with most of the packages,
  such as numpy and scipy.  If a newer version is required we can always
  add something as a module, via Anaconda or something other route.

8. [X] VSCode
  => Available as `code`; no module load required

9. [X] Intel oneapi base toolkit
  => Manually installed but with module files created into /opt/modulefiles/intel
  (via `/opt/intel/oneapi/modulefiles-setup.sh --output-dir=/opt/modulefiles/intel`)
  => Lots of installed modules now shown by `module avail`

10. [X] Intel HPC toolkit
  => Manually installed but with module files created into /opt/modulefiles/intel

11. [X] Nag Fortran libraries (for both Intel Fortran and GNU Fortran)

  From https://support.nag.com/content/downloads-nag-library these
  versions apply:

  + GNU gcc/gfortran version 8.1 or compatible
      -> https://support.nag.com/content/downloads-nag-library-nll6i27dgl (NLL6I27DG licence)

  + Fortran Compiler:    Intel Classic Fortran version 2021.4.0 and compatible
    C Compiler:  Intel Classic C/C++ version 2021.4.0 and compatible
    GNU C version 7.3 and compatible
      -> https://support.nag.com/content/downloads-nag-library-nll6i302nl (NLL6I30XN licence)

  + Fortran Compiler:    Intel Classic Fortran version 2021.4.0 and compatible
    Intel Classic Fortran version 19.0.5.281 and compatible
    C Compiler:  Intel Classic C/C++ version 2021.4.0 and compatible
    Intel Classic C/C++ version 19.0.5.281 and compatible
    GNU C version 10.3 and compatible
    GNU C version 11.2 and compatible
      -> https://support.nag.com/content/downloads-nag-library-nll6i302bl (NLL6I30XB licence)

  => Modules shown by `module avail`, but you'll need to load the
  appropriate Intel compiler/library modules as well.
  Note that `icc` is called `icx` now, so the examples compile but only
  when this is changed.  Perhaps an alias will fix this?

12. Graphical interface
    Thinlinc

    
You should also be able to use `x2go' to connect to the host, which
makes the connection over ssh but allows the use of a GUI remotely.
If you are on a managed host then hopefully this is available in the
Software Centre, but if not then it can be installed for various
platforms from https://wiki.x2go.org/doku.php/download%3Astart

I've ensured that the KDE desktop is available for use from x2go, but we
can add others as required.  (Note that GNOME will not work with x2go
because of some extensions it uses which are not supported by x2go)
