# SPDX-License-Identifier: GPL-3.0-only
#
# Copyright (C) 2023 ImmortalWrt.org
# Copyright (C) 2026 Internet1235

include $(TOPDIR)/rules.mk

PKG_NAME:=zeronews
PKG_VERSION:=3.0.2
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-openwrt-v2-$(PKG_VERSION).tar
ifeq ($(ARCH),aarch64)
  PKG_ARCH:=arm64
  PKG_HASH:=46f7ecd53ec613bbd89aa3bede4e3c681d16248fd87978159df3813f2ec5f3ee
else ifeq ($(ARCH),arm)
  PKG_ARCH:=arm
  PKG_HASH:=ef043db44f1d4e493de15247c3e7ee0eee5b00d4fec73820e2ef5fc451e53b14
else ifeq ($(ARCH),mips)
  PKG_ARCH:=mips
  PKG_HASH:=c7a8be9e2df51923a2bb64a09b3f7e991ce3e8e6c11c6bd8916c37ebc7580d8e
else ifeq ($(ARCH),x86_64)
  PKG_ARCH:=x86_x64
  PKG_HASH:=65302a2b38bccde77b35ef62327ec7678fb713f66c065ada7ca6e65c3064ed9d
endif
PKG_SOURCE_URL:=https://download.zeronews.cc/openwrt/$(PKG_ARCH)
PKG_BUILD_DIR:=$(BUILD_DIR)/zeronews

PKG_LICENSE:=Proprietary
PKG_MAINTAINER:=Internet1235

include $(INCLUDE_DIR)/package.mk

define Package/zeronews
  SECTION:=net
  CATEGORY:=Network
  TITLE:=ZeroNews Intranet Penetration
  DEPENDS:=@(aarch64||arm||mips||x86_64)
  URL:=https://zeronews.cc/
endef

define Package/zeronews/description
  ZeroNews is an innovative edge cloud intranet penetration platform 
  designed to help users quickly address the security and fast access 
  needs between intranet and internet.
endef

define Build/Compile
endef

define Package/zeronews/conffiles
/etc/config/zeronews
/etc/zeronews/
endef

define Package/zeronews/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/zeronews $(1)/usr/bin/zeronews

	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) $(CURDIR)/files/zeronews.init $(1)/etc/init.d/zeronews

	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_CONF) $(CURDIR)/files/zeronews.config $(1)/etc/config/zeronews
endef

$(eval $(call BuildPackage,zeronews))
