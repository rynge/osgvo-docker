FROM centos:6
MAINTAINER Mats Rynge "rynge@isi.edu"

RUN yum -y upgrade
RUN yum -y install epel-release yum-plugin-priorities

# osg repo
RUN yum -y install http://repo.grid.iu.edu/osg/3.3/osg-3.3-el6-release-latest.rpm
   
# pegasus repo 
RUN echo -e "# Pegasus\n[Pegasus]\nname=Pegasus\nbaseurl=http://download.pegasus.isi.edu/wms/download/rhel/6/\$basearch/\ngpgcheck=0\nenabled=1\npriority=50" >/etc/yum.repos.d/pegasus.repo

RUN yum -y groupinstall "Compute Node" "Compatibility Libraries" "Console Internet Tools" "Development Tools" "Scientific Support"
RUN yum -y install numpy scipy python-astropy astropy-tools
RUN yum -y install fontconfig libxml2 openssl098e libGLU libXpm binutils-devel gcc libgfortran python-devel subversion gcc-gfortran gcc-c++ binutils binutils-devel python-devel libxml2-devel mesa-libGL-devel glew-devel libX11-devel libXpm-devel libXft-devel libXext-devel glew mesa-libGL-devel which
    
# osg
RUN yum -y install osg-ca-certs osg-wn-client
RUN rm -f /etc/grid-security/certificates/*.r0

# htcondor - include so we can chirp
RUN yum -y install condor

# pegasus
RUN yum -y install pegasus

# required directories
RUN mkdir -p /cvmfs



