# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2022 Derek Watson

include $(TOPDIR)/rules.mk

PKG_NAME:=wolfMQTT
PKG_VERSION:=1.14.1
PKG_RELEASE:=$(AUTORELEASE)

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/wolfSSL/wolfMQTT/archive/v$(PKG_VERSION)
PKG_HASH:=43f76ca5116bef9b611233c8e1612fc88fab9380da1dbd50f64d64987eb3bea2

PKG_MAINTAINER:=Derek Watson
PKG_LICENSE:=GPL-2.0-or-later
PKG_LICENSE_FILES:=LICENSE
PKG_CPE_ID:=cpe:/a:wolfssl:wolfmqtt

PKG_FIXUP:=autoreconf
PKG_USE_MIPS16:=0
PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/wolfMQTT
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=MQTT library using wolfSSL
  MENU:=1
  DEPENDS:=+WOLFMQTT_HAS_TLS:libwolfssl
  URL:=https://github.com/wolfSSL/wolfMQTT
  ABI_VERSION:=$(PKG_ABI_VERSION)
endef

define Package/wolfMQTT/description
wolfMQTT is a client library implementation of the MQTT
protocol, written in ANSI C and targeted for embedded, RTOS,
and resource-constrained environments. It has been built from
the ground up to be multi-platform, space conscious, and
extensible. It includes support for the MQTT v5.0 protocol.
endef

define Package/wolfMQTT/config
	source "$(SOURCE)/Config.in"
endef

CONFIGURE_ARGS += \
  --disable-examples \
  --$(if $(CONFIG_WOLFMQTT_HAS_TLS),enable,disable)-tls \
  --$(if $(CONFIG_WOLFMQTT_HAS_V5),enable,disable)-v5 \
  --$(if $(CONFIG_WOLFMQTT_HAS_SN),enable,disable)-sn \
  --$(if $(CONFIG_WOLFMQTT_HAS_DEBUG),enable,disable)-debug \

define Build/Configure
	(cd $(PKG_BUILD_DIR); ./autogen.sh)
	$(call Build/Configure/Default)
endef

define Package/wolfMQTT/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libwolfmqtt.so.* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,wolfMQTT))
