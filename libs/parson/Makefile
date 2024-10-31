#
# Copyright (C) 2021 TDT AG <development@tdt.de>
#
# This is free software, licensed under the GNU General Public License v2.
# See https://www.gnu.org/licenses/gpl-2.0.txt for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=parson
PKG_VERSION:=1.5.2
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/kgabis/parson
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=60c37844d7a1c97547812cac3423d458c73e60f9
PKG_MIRROR_HASH:=1bfe84668dfa17d5c77f5d61edb7e0721ad7c9ef0b2ebe2c7f573314c7270a02

PKG_MAINTAINER:=Florian Eckert <fe@dev.tdt.de>
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/parson
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=Lighweight json library written in c
  URL:=https://github.com/kgabis/parson
  BUILDONLY:=1
endef

define Package/parson/description
Parson is a lighweight json library written in c.
Features:
* Full JSON support
* Lightweight (only 2 files)
* Simple API
* Addressing json values with dot notation
* C89 compatible
endef

CMAKE_BINARY_SUBDIR:=build

TARGET_CFLAGS += $(FPIC)

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/
	$(CP) $(PKG_INSTALL_DIR)/usr/include/*.h \
			$(1)/usr/include/

	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.a \
			$(1)/usr/lib/

	$(INSTALL_DIR) $(1)/usr/lib/cmake/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/cmake/* \
		$(1)/usr/lib/cmake/
endef

$(eval $(call BuildPackage,parson))
