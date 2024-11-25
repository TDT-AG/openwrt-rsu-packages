#
# Copyright (C) 2021 TDT AG <development@tdt.de>
#
# This is free software, licensed under the GNU General Public License v2.
# See https://www.gnu.org/licenses/gpl-2.0.txt for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=azure-iot-sdk-c
PKG_VERSION:=2024.08
PKG_REAL_VERSION:=LTS_08_2024
PKG_RELEASE:=2

PKG_SOURCE:=$(PKG_NAME)-$(PKG_REAL_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/Azure/azure-iot-sdk-c
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_REAL_VERSION)
PKG_MIRROR_HASH:=c0b3ac9fd3d97bf9c67b609196376a22dad24160aee2ebe59adcf14bc2c6fcb4

PKG_BUILD_DIR :=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

PKG_MAINTAINER:=Florian Eckert <fe@dev.tdt.de>
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE

PKG_BUILD_DEPENDS:= \
	azure-c-shared-utility \
	azure-uamqp-c \
	azure-umqtt-c \
	azure-uhttp-c \
	azure-utpm-c \
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
# depending on the cmake options, then this can lead to problems
# during compilation for other BUILD_VARIANT´s.
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
