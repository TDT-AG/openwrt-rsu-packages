#
# Copyright (C) 2023 TDT AG <development@tdt.de>
#
# This is free software, licensed under the GNU General Public License v2.
# See https://www.gnu.org/licenses/gpl-2.0.txt for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=azure-utpm-c
PKG_VERSION:=2024.05.28
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/Azure/azure-utpm-c
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=111a6c6ff7abe98951f60b633445f47e4ac5c0cd
PKG_MIRROR_HASH:=e4d5eba46423bf0e93e59467148aec45548833900f15969167842f8276ee7f84

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

define Package/azure-utpm-c
  SECTION:=libs
  CATEGORY:=Libraries
  SUBMENU:=Azure IoT
  TITLE:=Microsoft Azure IoT SDKs - TPM library for c
  URL:=https://github.com/Azure/azure-utpm-c
  BUILDONLY:=1
endef

define Package/azure-utpm-c/description
TPM C library for use with Azure IoT SDKs.
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
	$(INSTALL_DIR) $(1)/usr/include/azureiot/azure_utpm_c/
	$(CP) $(PKG_INSTALL_DIR)/usr/include/azureiot/azure_utpm_c/*.h \
		$(1)/usr/include/azureiot/azure_utpm_c/

	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.a \
		$(1)/usr/lib/

	$(INSTALL_DIR) $(1)/usr/cmake/
	$(CP) $(PKG_INSTALL_DIR)/usr/cmake/* \
		$(1)/usr/cmake/
endef

$(eval $(call BuildPackage,azure-utpm-c))
