#
# Copyright (C) 2021 TDT AG <development@tdt.de>
#
# This is free software, licensed under the GNU General Public License v2.
# See https://www.gnu.org/licenses/gpl-2.0.txt for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=oatpp
PKG_VERSION:=1.2.5
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/oatpp/oatpp/archive/$(PKG_VERSION)/
PKG_HASH:=36276e8b23e68ece1e6093c3f06fc80e3d42a5f4e47cdeef5e7e63f36eeddaad

PKG_MAINTAINER:=Florian Eckert <fe@dev.tdt.de>
PKG_LICENSE:=Apache-2.0
PKG_LICENSE_FILES:=LICENSE

CMAKE_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/oatpp
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=Oat++ is an open-source C++ web framework
  URL:=https://github.com/oatpp/oatpp.git
  DEPENDS:= +libatomic +libstdcpp
endef

define Package/oatpp/description
Oat++ is an open-source C++ web framework for highly scalable and
resource-efficient web applications. It provides all the necessary
components for production-grade development, including:

* Advanced REST framework with request parameters mapping and
  Swagger-UI annotations. See Api Controller and Api Client.
* ORM Framework. See Object-Relational Mapping (ORM)
* WebSocket framework. See 5-million connections benchmark.
* Object Mapping. See Data Transfer Object (DTO).
* Dependency Injection
* Swagger-UI. See oatpp-swagger module.

It's zero-dependency, easy-portable, and high-performance.
endef

CMAKE_BINARY_SUBDIR:=build_openwrt

CMAKE_OPTIONS+= \
	-DBUILD_SHARED_LIBS=ON \
	-DOATPP_BUILD_TESTS=OFF

define Package/oatpp/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/lib/$(PKG_NAME)-$(PKG_VERSION)/liboatpp.so \
		$(1)/usr/lib/
endef

$(eval $(call BuildPackage,oatpp))
