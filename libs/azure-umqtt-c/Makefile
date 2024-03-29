#
# Copyright (C) 2021 TDT AG <development@tdt.de>
#
# This is free software, licensed under the GNU General Public License v2.
# See https://www.gnu.org/licenses/gpl-2.0.txt for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=azure-umqtt-c
PKG_VERSION:=LTS_07_2022_Ref02
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/Azure/azure-umqtt-c
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_VERSION)
PKG_MIRROR_HASH:=1c0f88ca11ba3a1f20164ee66a5d623c35b9d33b15886b9000fcab153b011455

PKG_MAINTAINER:=Florian Eckert <fe@dev.tdt.de>
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE

# This packages are linked statically
PKG_BUILD_DEPENDS:= \
	macro-utils-c \
	umock-c \
	azure-c-shared-utility

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/azure-umqtt-c
  SECTION:=libs
  CATEGORY:=Libraries
  SUBMENU:=Azure IoT
  TITLE:=Microsoft Azure IoT SDKs - MQTT library for c
  URL:=https://github.com/Azure/azure-umqtt-c
  BUILDONLY:=1
  DEPENDS:= \
    +libuuid \
    +libopenssl \
    +libcurl
endef

define Package/azure-umqtt-c/description
This is a general purpose C library build for MQTT protocol.
endef

define Build/Prepare
	$(call Build/Prepare/Default)
	$(RM) -rf $(PKG_BUILD_DIR)/deps
endef

CMAKE_BINARY_SUBDIR:=build_openwrt

CMAKE_OPTIONS += \
		-Duse_installed_dependencies:bool=ON \
		-Drun_unittests:bool=OFF

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/azureiot/azure_umqtt_c/
	$(CP) $(PKG_INSTALL_DIR)/usr/include/azureiot/azure_umqtt_c/*.h \
		$(1)/usr/include/azureiot/azure_umqtt_c/

	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.a \
		$(1)/usr/lib/

	$(INSTALL_DIR) $(1)/usr/lib/cmake/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/cmake/* \
		$(1)/usr/lib/cmake/
endef

$(eval $(call BuildPackage,azure-umqtt-c))
