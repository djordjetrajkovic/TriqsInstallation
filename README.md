## *Triqs* installation


#### Debian/Ubuntu from package
Execute following commands:

	    sudo apt-get update
		sudo apt-get -y upgrade
		sudo apt-get update && sudo apt-get install -y software-properties-common apt-transport-https curl
##### For Ubuntu 18.04 (bionic):
		curl -L https://users.flatironinstitute.org/~ccq/triqs3/bionic/public.gpg | sudo apt-key add -
		sudo add-apt-repository "deb https://users.flatironinstitute.org/~ccq/triqs3/bionic/ /"
##### For Ubuntu 20.04 (focal):
	    curl -L https://users.flatironinstitute.org/~ccq/triqs3/focal/public.gpg | sudo apt-key add -
	    sudo add-apt-repository "deb https://users.flatironinstitute.org/~ccq/triqs3/focal/ /"
Continue with the following commands:

		sudo apt-get update && sudo apt-get install -y triqs
		sudo apt-get -y install cmake g++ gfortran git hdf5-tools libblas-dev libboost-dev libfftw3-dev libgfortran4 libgmp-dev libhdf5-dev liblapack-dev libopenmpi-dev python3-dev python3-mako python3-matplotlib python3-mpi4py python3-numpy python3-scipy
		sudo apt-get -y install jupyter-notebook
		sudo apt-get -y install clang libclang-dev
		sudo apt-get update && sudo apt-get install -y triqs
		sudo apt-get -y install clang libclang-dev net-tools firefox
		source /etc/lsb-release
		export CPLUS_INCLUDE_PATH=/usr/include/openmpi:/usr/include/hdf5/serial/:$CPLUS_INCLUDE_PATH
	
If no errors occur and installation was succesfull, directory */usr/lib/python3.**x**/dist-packages/* has the following structure:
```
	drwxr-xr-x  2 root root 4.0K Aug 24 17:47 cpp2cxx
	drwxr-xr-x  3 root root 4.0K Aug 24 17:47 cpp2py
	drwxr-xr-x  2 root root 4.0K Aug 24 17:47 cpp2rst
	drwxr-xr-x  2 root root 4.0K Aug 24 17:47 h5
	drwxr-xr-x 15 root root 4.0K Aug 24 17:47 triqs
```
>Where **x** is minor python version number.

Now, create virtual environment with the following parameter:
```
	python3 -m virtualenv venv --system-site-packages
```

#### Debian/Ubuntu from source
Execute the following commands:

		sudo apt-get update
		sudo apt-get -y upgrade
		sudo apt-get -y install cmake g++ gfortran git hdf5-tools libblas-dev libboost-dev libfftw3-dev libgfortran4 libgmp-dev libhdf5-dev liblapack-dev libopenmpi-dev      python3-dev python3-mako python3-matplotlib python3-mpi4py python3-numpy python3-scipy
		sudo apt-get -y install jupyter-notebook
		cd ~ && mkdir triqs && cd triqs/
		touch install.bash
Now, insert text and make script executable:
		
		cat > install.bash
		
		#!/bin/bash

		# Set this variable to your desired install directory
		INSTALL_PREFIX=$(pwd)/install

		# Set the number of cores for the compilation
		NCORES=4

		# Clone the git repository of triqs
		git clone https://github.com/TRIQS/triqs triqs.src

		# Use cmake to configure the triqs build process
		mkdir -p triqs.build && cd triqs.build
		cmake ../triqs.src -DCMAKE_INSTALL_PREFIX=$INSTALL_PREFIX

		# Build, test and install triqs
		make -j$NCORES && make test && make install
		cd ../

		# Load the triqs installation into your environment
		source $INSTALL_PREFIX/share/triqsvars.sh

		echo 
		echo "If you want to automatically load triqs into your environment,"
		echo "please add the following line to your ~/.bash_profile (or ~/.zprofile):"
		echo "source $INSTALL_PREFIX/share/triqsvars.sh"

Execute script:
		
		chmod +x install.bash
		./install.bash
After finishing, installation should be placed in */home/\$USER/triqs* folder.

Now it's necessery to make script */home/$USER/triqs/install/share/triqsvars.sh* executable when logging so put command: *source /home/\$USER/triqs/install/share/triqsvars.sh* in the *~/.bashrc* file in your */home* folder.

Log out and log in again.
