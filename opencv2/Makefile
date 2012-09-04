# point these to your cuda install
CUDA_TOOLKIT_ROOT_DIR = /usr/local/cuda
CUDA_SDK_ROOT_DIR = /wg/stor5/jbinney/ws/people_tracking/install/gpu_sdk

# leave these alone
OPENCV_PKG_DIR = $(shell rospack find opencv2)
SRC_DIR = $(OPENCV_PKG_DIR)/src
BUILD_DIR = $(OPENCV_PKG_DIR)/build
INSTALL_DIR = $(OPENCV_PKG_DIR)/install

vcs_clone :
	mkdir $(SRC_DIR)
	git clone https://github.com/Itseez/opencv $(SRC_DIR)

configure :
	cd $(BUILD_DIR)
	cmake -D CMAKE_INSTALL_PREFIX=/usr/local -D WITH_TBB=ON -D WITH_CUDA=ON -D CUDA_TOOLKIT_ROOT_DIR=/usr/local/cuda -D CUDA_SDK_ROOT_DIR=/<Your path to the nvidia sdk>/NVIDIA_GPU_Computing_SDK ..
make
	cd -

build : configure
	cd $(BUILD_DIR)
	make -j8
	cd -

install : build
	mkdir -p $(INSTALL_DIR)
	cd $(BUILD_DIR)
	make install