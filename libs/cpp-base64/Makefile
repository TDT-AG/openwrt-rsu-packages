#
# Copyright (C) 2021 TDT AG <development@tdt.de>
#
# This is free software, licensed under the GNU General Public License v2.
# See https://www.gnu.org/licenses/gpl-2.0.txt for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=cpp-base64
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/ReneNyffenegger/cpp-base64
PKG_SOURCE_DATE:=2021-08-06
PKG_SOURCE_VERSION:=c65b936453d7cbf9c585806142cd866b7bc7c0d5
PKG_MIRROR_HASH:=1bd407ab5e5731a11bf1eeea77a6a9d05181d26444491b8e57c13415d57ceea8

PKG_MAINTAINER:=Florian Eckert <fe@dev.tdt.de>
PKG_LICENSE:=Zlib
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/cpp-base64
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=Base64 encoding and decoding with C++
  URL:=https://github.com/ReneNyffenegger/cpp-base64.git
  BUILDONLY:=1
endef

define Package/cpp-base64/description
 Base64 encoding and decoding with c++
endef

CMAKE_BINARY_SUBDIR:=build_openwrt

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/
	$(CP) $(PKG_BUILD_DIR)/base64.h \
		$(1)/usr/include/

	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/* \
		$(1)/usr/lib/
endef

$(eval $(call BuildPackage,cpp-base64))
