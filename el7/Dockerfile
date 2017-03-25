FROM centos:7
MAINTAINER Mats Rynge "rynge@isi.edu"

RUN yum -y upgrade
RUN yum -y install epel-release yum-plugin-priorities

# osg repo
RUN yum -y install http://repo.grid.iu.edu/osg/3.3/osg-3.3-el7-release-latest.rpm
   
# pegasus repo 
RUN echo -e "# Pegasus\n[Pegasus]\nname=Pegasus\nbaseurl=http://download.pegasus.isi.edu/wms/download/rhel/7/\$basearch/\ngpgcheck=0\nenabled=1\npriority=50" >/etc/yum.repos.d/pegasus.repo

# well rounded basic system to support a wide range of user jobs
RUN yum -y groups mark convert \
    && yum -y grouplist \
    && yum -y groupinstall "Compatibility Libraries" \
                           "Development Tools" \
                           "Scientific Support"

RUN yum -y install tcsh wget curl rsync which time bc octave octave-devel \
                   libtool libtool-ltdl libtool-ltdl-devel \
                   fontconfig libxml2 openssl098e libGLU libXpm \
                   gcc libgfortran libgomp \
                   subversion git gcc-gfortran gcc-c++ binutils binutils-devel \
                   libquadmath libicu \
                   python-devel libxml2-devel mesa-libGL-devel \
                   numpy scipy python-astropy astropy-tools \
                   glew-devel libX11-devel libXpm-devel libXft-devel libXt \
                   libXaw-devel libXext-devel libXmu-devel tk-devel tcl-devel \
                   glib-devel glib2-devel gsl-devel \
                   java-1.8.0-openjdk java-1.8.0-openjdk-devel \
                   R-devel graphviz
    
# osg
# use CA certs from CVMFS
RUN yum -y install osg-ca-certs osg-wn-client \
    && mv /etc/grid-security/certificates /etc/grid-security/certificates.osg-ca-certs \
    && ln -s /cvmfs/oasis.opensciencegrid.org/mis/certificates /etc/grid-security/certificates

# htcondor - include so we can chirp
RUN yum -y install condor

# pegasus
RUN yum -y install pegasus

# required directories
RUN mkdir -p /cvmfs

# verification
RUN ls -l /etc/grid-security/

# build info
RUN echo "Timestamp:" `date --utc` | tee /image-build-info.txt

