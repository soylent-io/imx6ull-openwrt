#
# Copyright (C) 2007-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=tensorflow
PKG_VERSION:=1
PKG_RELEASE:=
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)


CMAKE_BINARY_SUBDIR=tensorflow-sdk-build
SOURCE_SUBDIR=tensorflow-sdk-source
CMAKE_SOURCE_SUBDIR=tensorflow-sdk-source/tensorflow/lite/examples/minimal

CMAKE_OPTIONS=-DCMAKE_BUILD_TYPE=MINSIZEREL -DCMAKE_SYSTEM_PROCESSOR=armv7 #-DTFLITE_ENABLE_XNNPACK=OFF

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/tensorflow
  SECTION:=tensorflow
  CATEGORY:=Examples
  TITLE:=tensorflow
  DEPENDS:=+libstdcpp
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)/$(CMAKE_BINARY_SUBDIR)
	mkdir -p $(PKG_BUILD_DIR)/$(SOURCE_SUBDIR)
	$(CP) ./src/* $(PKG_BUILD_DIR)/$(SOURCE_SUBDIR)/
	$(MAKE) --version
	cmake --version
	whereis cmake
endef

define Package/tensorflow/description
 Tensorflow-lite for embedded linux minimal working example.
endef

define Build/Configure
	$(Build/Configure/Default)
	$(Build/Patch)
endef

define Build/Compile
	$(MAKE_VARS) $(MAKE) $(PKG_JOBS) -C $(PKG_BUILD_DIR)/$(CMAKE_BINARY_SUBDIR) $(MAKE_FLAGS)
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/tensorflow $(1)/usr/include/tensorflow/lite
	$(CP) $(PKG_BUILD_DIR)/$(SOURCE_SUBDIR)/tensorflow/lite/*.h $(1)/usr/include/tensorflow/lite
	$(INSTALL_DIR) $(1)/usr/include/tensorflow/lite/core
	$(CP) $(PKG_BUILD_DIR)/$(SOURCE_SUBDIR)/tensorflow/lite/core/*.h $(1)/usr/include/tensorflow/lite/core
	$(INSTALL_DIR) $(1)/usr/include/tensorflow/lite/core/api
	$(CP) $(PKG_BUILD_DIR)/$(SOURCE_SUBDIR)/tensorflow/lite/core/api/*.h $(1)/usr/include/tensorflow/lite/core/api
	$(INSTALL_DIR) $(1)/usr/include/tensorflow/lite/c/
	$(CP) $(PKG_BUILD_DIR)/$(SOURCE_SUBDIR)/tensorflow/lite/c/*.h $(1)/usr/include/tensorflow/lite/c/
	$(INSTALL_DIR) $(1)/usr/include/tensorflow/lite/experimental/resource
	$(CP) $(PKG_BUILD_DIR)/$(SOURCE_SUBDIR)/tensorflow/lite/experimental/resource/*.h $(1)/usr/include/tensorflow/lite/experimental/resource
	$(INSTALL_DIR) $(1)/usr/include/tensorflow/lite/kernels
	$(CP) $(PKG_BUILD_DIR)/$(SOURCE_SUBDIR)/tensorflow/lite/kernels/*.h $(1)/usr/include/tensorflow/lite/kernels
	$(INSTALL_DIR) $(1)/usr/include/tensorflow/lite/kernels/internal
	$(CP) $(PKG_BUILD_DIR)/$(SOURCE_SUBDIR)/tensorflow/lite/kernels/internal/*.h $(1)/usr/include/tensorflow/lite/kernels/internal
	$(INSTALL_DIR) $(1)/usr/include/tensorflow/lite/schema
	$(CP) $(PKG_BUILD_DIR)/$(SOURCE_SUBDIR)/tensorflow/lite/schema/*.h $(1)/usr/include/tensorflow/lite/schema
	$(INSTALL_DIR) $(1)/usr/include/flatbuffers
	$(CP) $(PKG_BUILD_DIR)/$(CMAKE_BINARY_SUBDIR)/flatbuffers/include/flatbuffers/*.h $(1)/usr/include/flatbuffers/
	$(INSTALL_DIR) $(1)/etc/tensorflow $(1)/usr/lib $(1)/bin
	$(CP) $(PKG_BUILD_DIR)/$(CMAKE_BINARY_SUBDIR)/tensorflow-lite/libtensorflow-lite.a $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/$(CMAKE_BINARY_SUBDIR)/_deps/xnnpack-build/libXNNPACK.a $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/$(CMAKE_BINARY_SUBDIR)/cpuinfo/libcpuinfo.a $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/$(CMAKE_BINARY_SUBDIR)/clog/libclog.a $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/$(CMAKE_BINARY_SUBDIR)/pthreadpool/libpthreadpool.a $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/$(CMAKE_BINARY_SUBDIR)/_deps/ruy-build/libruy.a $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/$(CMAKE_BINARY_SUBDIR)/_deps/flatbuffers-build/libflatbuffers.a $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/$(CMAKE_BINARY_SUBDIR)/_deps/fft2d-build/libfft2d_fftsg*.a $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/$(CMAKE_BINARY_SUBDIR)/_deps/farmhash-build/libfarmhash.a $(1)/usr/lib
#	$(CP) $(PKG_INSTALL_DIR)/usr/lib/* $(1)/usr/lib/
	$(CP) ./files/* $(1)/
	$(STRIP) $(PKG_BUILD_DIR)/$(CMAKE_BINARY_SUBDIR)/minimal
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/$(CMAKE_BINARY_SUBDIR)/minimal $(1)/bin/
endef

define Package/tensorflow/install
	$(INSTALL_DIR) $(1)/etc/tensorflow $(1)/usr/lib $(1)/bin
#	$(CP) $(PKG_INSTALL_DIR)/usr/lib/* $(1)/usr/lib/
	$(CP) ./files/* $(1)/
	$(STRIP) $(PKG_BUILD_DIR)/$(CMAKE_BINARY_SUBDIR)/minimal
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/$(CMAKE_BINARY_SUBDIR)/minimal $(1)/bin/
endef

$(eval $(call BuildPackage,tensorflow,+libstdcpp))
