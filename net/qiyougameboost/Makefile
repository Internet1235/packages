# SPDX-License-Identifier: GPL-2.0-only
#

include $(TOPDIR)/rules.mk

PKG_NAME:=qiyougameboost
PKG_VERSION:=1.2.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://static.qiyou.cn/upgrade/ljb/plugin/QYPLUG_SYS_X86X2_$(PKG_VERSION).tar.gz?
PKG_HASH:=6d392fd4aae04590b4040b224d1c500f694d7109393f674d902ff9d2a1551992
PKG_BUILD_DIR:=$(BUILD_DIR)/qy

PKG_LICENSE:=Proprietary
PKG_MAINTAINER:=qiyouacc, Internet1235

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
  SECTION:=net
  CATEGORY:=Network
  TITLE:=QiYou Game Boost
  DEPENDS:=+kmod-tun +curl
  URL:=https://www.qiyou.cn
endef

define Package/$(PKG_NAME)/description
  Play console games online with less lag and more stability 
  — now supporting PS, Switch, Xbox, PC, and mobile.
endef

define Build/Compile
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/bin/qy_acc $(1)/usr/bin/qiyougameboost

	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) files/qiyougameboost.init $(1)/etc/init.d/qiyougameboost

	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_CONF) files/qiyougameboost.config $(1)/etc/config/qiyougameboost
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
