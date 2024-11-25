#
# Copyright (C) 2021 TDT AG <development@tdt.de>
#
# This is free software, licensed under the GNU General Public License v2.
# See https://www.gnu.org/licenses/gpl-2.0.txt for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=rapidjson
PKG_VERSION:=2024.10.07
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/Tencent/rapidjson.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=858451e5b7d1c56cf8f6d58f88cf958351837e53
PKG_MIRROR_HASH:=241ffd60d1341743cf611aa40fb63bf7d95ff795a1da543898525a3b734e3bac

PKG_MAINTAINER:=Florian Eckert <fe@dev.tdt.de>
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=license.txt

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/rapidjson
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=JSON parser/generator for C++
  URL:=https://github.com/Tencent/rapidjson.git
  BUILDONLY:=1
endef

define Package/rapidjson/description
 A fast JSON parser/generator for C++ with both SAX/DOM style API
endef

CMAKE_OPTIONS += \
	-DRAPIDJSON_BUILD_DOC=OFF \
	-DRAPIDJSON_BUILD_EXAMPLES=OFF \
	-DRAPIDJSON_BUILD_TESTS=OFF

CMAKE_BINARY_SUBDIR:=build_openwrt

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/rapidjson
	$(CP) $(PKG_INSTALL_DIR)/usr/include/rapidjson/* \
		$(1)/usr/include/rapidjson/

	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/* \
		$(1)/usr/lib/
endef

$(eval $(call BuildPackage,rapidjson))
