# SPDX-License-Identifier: GPL-2.0-only
#

include $(TOPDIR)/rules.mk

PKG_NAME:=qiyougamebooster
PKG_VERSION:=1.2.0
PKG_RELEASE:=1

ifeq ($(ARCH), aarch64)
  PKG_ARCH:=SYS_ARMX1
else ifeq ($(ARCH), arm)
  PKG_ARCH:=SYS_ARMX2
else ifeq ($(ARCH), mips)
  PKG_ARCH:=SYS_MIPSX1
else ifeq ($(ARCH), mipsel)
  PKG_ARCH:=SYS_MIPSX2
else ifeq ($(ARCH), i386)
  PKG_ARCH:=SYS_X86X1
else ifeq ($(ARCH), x86_64)
  PKG_ARCH:=SYS_X64X1
endif

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(ARCH).tar.gz
PKG_SOURCE_URL:=https://static.qiyou.cn/upgrade/ljb/plugin/QYPLUG_$(PKG_ARCH)_$(PKG_VERSION).tar.gz?
PKG_HASH:=skip
PKG_BUILD_DIR:=$(BUILD_DIR)/qy


PKG_LICENSE:=Proprietary
PKG_MAINTAINER:=qiyouacc, Internet1235

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
  SECTION:=net
  CATEGORY:=Network
  TITLE:=QiYou Game Booster
  DEPENDS:=@(aarch64||arm||mips||mipsel||i386||x86_64) +curl +ip-full +kmod-tun
  URL:=https://www.qiyou.cn
endef

define Package/$(PKG_NAME)/description
  Play console games online with less lag and more stability
  — now supporting PS, Switch, Xbox, PC, and mobile.
endef

define Build/Compile
endef

define Package/$(PKG_NAME)/conffiles
/etc/config/qiyougamebooster
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/bin/qy_acc $(1)/usr/bin/qiyougamebooster
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/bin/qy_mosq $(1)/usr/bin/qy_mosq
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/bin/qy_proxy $(1)/usr/bin/qy_proxy

	$(INSTALL_DIR) $(1)/usr/share/qiyougamebooster
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/etc/PKG_INFO $(1)/usr/share/qiyougamebooster/PKG_INFO

	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) $(CURDIR)/files/qiyougamebooster.init $(1)/etc/init.d/qiyougamebooster

	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_CONF) $(CURDIR)/files/qiyougamebooster.config $(1)/etc/config/qiyougamebooster

	$(INSTALL_DIR) $(1)/usr/lib/qiyougamebooster
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
