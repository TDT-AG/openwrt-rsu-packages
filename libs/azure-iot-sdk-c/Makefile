#
# Copyright (C) 2021 TDT AG <development@tdt.de>
#
# This is free software, licensed under the GNU General Public License v2.
# See https://www.gnu.org/licenses/gpl-2.0.txt for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=azure-iot-sdk-c
PKG_VERSION:=LTS_01_2021_Ref01
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/Azure/azure-iot-sdk-c
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=17b7d536485b5e69555d76074803495b7b18e7ab
PKG_MIRROR_HASH:=f49744038a4fbec7c528fe8ab80df4abe775128d8b97a75ca5572a5debf09109

PKG_MAINTAINER:=Florian Eckert <fe@dev.tdt.de>
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE

# This packages are linked statically
PKG_BUILD_DEPENDS:= \
	azure-c-shared-utility \
	azure-uamqp-c \
	azure-umqtt-c \
	azure-uhttp-c \
	parson \
	macro-utils-c \
	umock-c

CMAKE_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/azure-iot-sdk-c/default
  SECTION:=libs
  CATEGORY:=Libraries
  SUBMENU:=Azure IoT
  TITLE:=Microsoft Azure IoT SDK -
  URL:=https://github.com/Azure/azure-iot-sdk-c
  DEPENDS:= \
    +libopenssl \
    +libuuid \
    +libcurl
endef

define Package/iothub-client
  $(call Package/azure-iot-sdk-c/default)
  TITLE+= client library
endef

define Package/iothub-client/description
	Library for iothub-client
endef

define Package/prov-device-client/description
	Library for client provision
endef

define Package/prov-device-client
  $(call Package/azure-iot-sdk-c/default)
  TITLE+= provision library
endef

define Build/Prepare
	$(call Build/Prepare/Default)
	$(RM) -rf $(PKG_BUILD_DIR)/deps
	$(RM) -rf $(PKG_BUILD_DIR)/c-utility
	$(RM) -rf $(PKG_BUILD_DIR)/uamqp
	$(RM) -rf $(PKG_BUILD_DIR)/umqtt
	$(RM) -rf $(PKG_BUILD_DIR)/provisioning_client/deps
endef

CMAKE_BINARY_SUBDIR:=build_openwrt

CMAKE_OPTIONS += \
		-Duse_amqp=ON \
		-Duse_http=ON \
		-Duse_mqtt=ON \
		-Dhsm_type_custom=ON \
		-Duse_prov_client=ON \
		-Duse_installed_dependencies=ON \
		-Dskip_samples=ON \
		-Dbuild_as_dynamic=ON

define Package/iothub-client/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libiothub_client.so.* \
		$(1)/usr/lib/
endef

define Package/prov-device-client/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libprov_device_client.so.* \
		$(1)/usr/lib/
endef

$(eval $(call BuildPackage,iothub-client))
$(eval $(call BuildPackage,prov-device-client))
