#
# Copyright (C) 2010-2016 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libedgetpu
PKG_RELEASE:=0

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/google-coral/libedgetpu.git
PKG_MIRROR_HASH:=358f575270508c783e3021df0688e34fc8e476caa06b2a414d9fcbc3175b52fb
PKG_SOURCE_DATE:=2021-05-05
PKG_SOURCE_VERSION:=efb73cc94dac29dc590a243109d4654c223e008c

include $(INCLUDE_DIR)/package.mk

define Package/libedgetpu
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=The Edge TPU Runtime (libedgetpu)
  DEPENDS:=+librt +libpthread +tensorflow
  ABI_VERSION:=0
endef

define Build/Prepare
	$(Build/Prepare/Default)
	$(CP) files/GNUmakefile $(PKG_BUILD_DIR)/
	$(CP) files/api/driver_options_generated.h $(PKG_BUILD_DIR)/api
	$(CP) files/executable/executable_generated.h $(PKG_BUILD_DIR)/executable
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_BUILD_DIR)/tflite/public/edgetpu*.h $(1)/usr/include/
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/libedgetpu_direct.so $(1)/usr/lib/
endef

define Package/libedgetpu/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/libedgetpu_direct.so $(1)/usr/lib/
endef

$(eval $(call BuildPackage,libedgetpu))
