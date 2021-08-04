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

PKG_BUILD_DEPENDS:= \
	azure-c-shared-utility \
	azure-uamqp-c \
	azure-umqtt-c \
	azure-uhttp-c \
	parson \
	macro-utils-c \
	umock-c

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/iothub-client/default
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

define Package/iothub-client-hsm-type-no
  $(call Package/iothub-client/default)
  TITLE+= client library without hsm
  VARIANT:=iothub-client-hsm-type-no
  CONFLICTS:=iothub-client-hsm-type-custom
  PROVIDES:=iothub-client
endef

define Package/iothub-client-hsm-type-no/description
	Library for iothub-client without hsm
endef

define Package/iothub-client-hsm-type-custom
  $(call Package/iothub-client/default)
  TITLE+= client library with hsm type custom
  VARIANT:=iothub-client-hsm-type-custom
  PROVIDES:=iothub-client
endef

define Package/iothub-client-hsm-type-custom/description
	Library for iothub-client with custom hsm
endef

define Build/Prepare
	$(call Build/Prepare/Default)
	$(RM) -rf $(PKG_BUILD_DIR)/deps
	$(RM) -rf $(PKG_BUILD_DIR)/c-utility
	$(RM) -rf $(PKG_BUILD_DIR)/uamqp
	$(RM) -rf $(PKG_BUILD_DIR)/umqtt
	$(RM) -rf $(PKG_BUILD_DIR)/provisioning_client/deps
endef

CMAKE_OPTIONS += \
	-Duse_amqp=ON \
	-Duse_http=ON \
	-Duse_mqtt=ON \
	-Duse_installed_dependencies=ON \
	-Dskip_samples=ON \
	-Dbuild_as_dynamic=OFF \
	-Dbuild_service_client=OFF \
	-Dbuild_provisioning_service_client=OFF

ifeq ($(BUILD_VARIANT),iothub-client-hsm-type-no)
  CMAKE_BINARY_SUBDIR:=build_openwrt-hsm-type-no
endif

ifeq ($(BUILD_VARIANT),iothub-client-hsm-type-custom)
  CMAKE_BINARY_SUBDIR:=build_openwrt-hsm-type-custom
  CMAKE_OPTIONS += -Dhsm_type_custom=ON -Duse_prov_client=ON
endif

# FIXME:
# The includes are installed for all BUILD_VARIANTs.
# If the cmake install target for the include headers differs,
# depending on the cmake options, then this can lead to problmes
# during compilation for other BUILD_VARIANTs.
define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/* \
		$(1)/usr/include/

	$(INSTALL_DIR) $(1)/usr/lib/azure-$(BUILD_VARIANT)/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/* \
		$(1)/usr/lib/azure-$(BUILD_VARIANT)/
endef

$(eval $(call BuildPackage,iothub-client-hsm-type-no))
$(eval $(call BuildPackage,iothub-client-hsm-type-custom))
