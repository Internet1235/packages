#
# Copyright (C) 2017-2024
#
# This is free software, licensed under the GNU General Public License v2.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=clouddrive2
PKG_VERSION:=0.8.17
PKG_RELEASE=1

ifeq ($(ARCH),aarch64)
	PKG_ARCH:=aarch64
	PKG_HASH:=d0df83d1b6b7f83eb17e25bc4635755c74dcca92e21b2bae1d914ea984b72591
else ifeq ($(ARCH),arm)
	PKG_ARCH:=armv7
	PKG_HASH:=b706c43f175790d96189181ed8a7c57c91cf835b07ebe50d9c15260fbfc6fb19
else ifeq ($(ARCH),x86_64)
	PKG_ARCH:=x86_64
	PKG_HASH:=8f740927a705f9d728b643097036d6d6b7f511375fa1f893a2d0dc57e6c7f336
endif

include $(INCLUDE_DIR)/package.mk

define Package/clouddrive2
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=@(arm||aarch64||x86_64) +fuse-utils
  TITLE:=CloudDrive2
endef

define Package/clouddrive2/description
  CloudDrive2 is a cloud storage mounting tool for OpenWrt.
endef

PKG_SOURCE:=clouddrive-2-linux-$(PKG_ARCH)-$(PKG_VERSION).tgz
PKG_SOURCE_URL:=https://github.com/cloud-fs/cloud-fs.github.io/releases/download/v$(PKG_VERSION)

define Build/Prepare
	$(call Build/Prepare/Default)
	tar -xzvf $(DL_DIR)/clouddrive-2-linux-$(PKG_ARCH)-$(PKG_VERSION).tgz -C $(PKG_BUILD_DIR)/ --strip-components=1
endef

define Build/Compile
endef

define Package/clouddrive2/install
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/clouddrive2.init $(1)/etc/init.d/clouddrive2
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_CONF) ./files/clouddrive2.config $(1)/etc/config/clouddrive2
	$(INSTALL_DIR) $(1)/usr/share/clouddrive2
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/clouddrive-2-linux-$(PKG_ARCH)-$(PKG_VERSION)/clouddrive $(1)/usr/share/clouddrive2/
	cp -rf $(PKG_BUILD_DIR)/clouddrive-2-linux-$(PKG_ARCH)-$(PKG_VERSION)/wwwroot $(1)/usr/share/clouddrive2/
endef

$(eval $(call BuildPackage,clouddrive2))
