#
# Copyright (C) 2021 TDT AG <development@tdt.de>
#
# This is free software, licensed under the GNU General Public License v2.
# See https://www.gnu.org/licenses/gpl-2.0.txt for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=cpp-base64
PKG_VERSION:=2022.11.01
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/ReneNyffenegger/cpp-base64
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=82147d6d89636217b870f54ec07ddd3e544d5f69
PKG_MIRROR_HASH:=216b5a7fa049078e440eee4784d241b663dadf34cf53822d52abd5d7d9f01488

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
