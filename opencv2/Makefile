# point these to your cuda install
CUDA_TOOLKIT_ROOT_DIR = /usr/local/cuda
CUDA_SDK_ROOT_DIR = /wg/stor5/jbinney/ws/people_tracking/install/gpu_sdk

# leave these alone
OPENCV_PKG_DIR = $(shell rospack find opencv2)
SRC_DIR = $(OPENCV_PKG_DIR)/src
BUILD_DIR = $(OPENCV_PKG_DIR)/build
INSTALL_DIR = $(OPENCV_PKG_DIR)/install

install : build
	mkdir -p $(INSTALL_DIR)
	cd $(BUILD_DIR) && make install && cd -

vcs_clone :
	mkdir -p $(SRC_DIR)
	git clone https://github.com/Itseez/opencv $(SRC_DIR)

configure :
	mkdir -p $(BUILD_DIR)
	cd $(BUILD_DIR); \
	CUDA_LIB_PATH=/usr/lib/nvidia-current cmake -D CMAKE_INSTALL_PREFIX=$(INSTALL_DIR) -D WITH_TBB=ON -D WITH_CUDA=ON -D CUDA_TOOLKIT_ROOT_DIR=${CUDA_TOOLKIT_ROOT_DIR} -D CUDA_SDK_ROOT_DIR=${CUDA_SDK_ROOT_DIR} $(SRC_DIR); \
	cd -

build : configure
	cd $(BUILD_DIR) && $(ENV_VARS) make -j8 && cd -

echo_vars :
	echo "CUDA_TOOLKIT_DIR : " $(CUDA_TOOLKIT_ROOT_DIR);
	echo "CUDA_SDK_DIR : " $(CUDA_SDK_ROOT_DIR);
	echo "SRC_DIR : " $(SRC_DIR)
	echo "BUILD_DIR : " $(BUILD_DIR)
	echo "INSTALL_DIR : " $(INSTALL_DIR)


