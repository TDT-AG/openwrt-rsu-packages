#
# Copyright (C) 2021 TDT AG <development@tdt.de>
#
# This is free software, licensed under the GNU General Public License v2.
# See https://www.gnu.org/licenses/gpl-2.0.txt for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=rsu-connector
PKG_VERSION:=2021-08-04
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_HASH:=ce45d53b382461a3f9589cc140904d83ad4867284c50cb5201b6274d9476343a

PKG_MAINTAINER:=Florian Eckert <fe@dev.tdt.de>
PKG_USE_NINJA:=0
#PKG_LICENSE:=LGPL-2.0
#PKG_LICENSE_FILES:=COPYING

PKG_BUILD_DEPENDS:= \
	rapidjson \
	cpp-base64 \
	spdlog \
	azure-iot-sdk-c

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/rsu-connector/default
  SECTION:=net
  CATEGORY:=Network
  TITLE:=Remote Service Unit -
  DEPENDS:= \
    +libstdcpp \
    +libatomic \
    +libubox \
    +libubus \
    +libuci \
    +azure-c-shared-utility \
    +libfmt \
    +oatpp
endef

define Package/rsu-connector
  $(call Package/rsu-connector/default)
  TITLE+= Azure IoT connector
endef

define Package/rsu-connector/description
Azure IoT connector for the Remote Service Unit (RSU).
endef

define Package/rsu-forwarder
  $(call Package/rsu-connector/default)
  TITLE+= Telemetry forwarder
endef

define Package/rsu-forwarder/description
Telemetry forwarder for the Remote Service Unit (RSU).
endef

define Package/rsu-connector/conffiles
/etc/config/rsu
endef

define Build/Prepare
	$(call Build/Prepare/Default)
	$(RM) -rf $(PKG_BUILD_DIR)/CMakeLists.txt
	$(CP) ./src/CMakeLists.txt \
		$(PKG_BUILD_DIR)/CMakeLists.txt
endef

CMAKE_BINARY_SUBDIR:=build_openwrt

TARGET_CFLAGS += -DSPDLOG_FMT_EXTERNAL

define Package/rsu-connector/install
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/etc/init.d/rsu-connector \
		$(1)/etc/init.d/

	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/rsu-connector \
		$(1)/usr/bin/

	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_CONF) ./files/etc/config/rsu \
		$(1)/etc/config/rsu
endef

define Package/rsu-forwarder/install
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/etc/init.d/rsu-forwarder \
		$(1)/etc/init.d/

	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/rsu-forwarder \
		$(1)/usr/bin/
endef

$(eval $(call BuildPackage,rsu-connector))
$(eval $(call BuildPackage,rsu-forwarder))
