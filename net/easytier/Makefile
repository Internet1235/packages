include $(TOPDIR)/rules.mk

PKG_NAME:=easytier
PKG_VERSION:=2.5.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/EasyTier/EasyTier/tar.gz/v$(PKG_VERSION)?
PKG_HASH:=ed3f3ad4eb08c11588660eb90239e1f548f8f724718ec27779cb09825ec3ac8e
PKG_BUILD_DIR:=$(BUILD_DIR)/EasyTier-$(PKG_VERSION)

PKG_LICENSE:=LGPL-3.0-only
PKG_LICENSE_FILES:=LICENSE

PKG_BUILD_DEPENDS:=rust/host protobuf/host
PKG_BUILD_PARALLEL:=1
PKG_USE_MIPS16:=0

include $(INCLUDE_DIR)/package.mk
include ../../lang/rust/rust-package.mk

define Package/easytier
	SECTION:=net
	CATEGORY:=Network
	TITLE:=A simple, decentralized mesh VPN with WireGuard support.
	DEPENDS:=$(RUST_ARCH_DEPENDS) +kmod-tun +libatomic
	URL:=https://github.com/EasyTier/EasyTier
endef

define Package/easytier/description
  A simple, decentralized mesh VPN with WireGuard support.
endef

WEB_FILE:=$(PKG_NAME)-web-v$(PKG_VERSION).zip
define Download/easytier-web
	URL:=https://github.com/EasyTier/EasyTier/releases/download/v$(PKG_VERSION)/
	URL_FILE:=easytier-web-dashboard-v$(PKG_VERSION).zip
	FILE:=$(WEB_FILE)
	HASH:=2ce6fa43bca5eba5a5f7bd20a1ffd2e17637a07c23c2364b37b2a5244bda611c
endef

define Build/Prepare
	$(call Build/Prepare/Default)

	( \
		mkdir -p $(PKG_BUILD_DIR)/easytier-web/frontend/dist ; \
		unzip -q -j -d $(PKG_BUILD_DIR)/easytier-web/frontend/dist $(DL_DIR)/$(WEB_FILE) ; \
	)
endef

CARGO_PKG_VARS += PROTOC=$(STAGING_DIR_HOSTPKG)/bin/protoc
CARGO_RUSTFLAGS += -C link-args=-latomic

define Build/Compile
	$(call Build/Compile/Cargo,easytier)
	$(call Build/Compile/Cargo,easytier-web,--features=embed)
endef

define Package/easytier/install
	$(INSTALL_DIR) $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/bin/{easytier-core,easytier-cli,easytier-web} $(1)/usr/bin/
endef

$(eval $(call Download,easytier-web))
$(eval $(call RustBinPackage,easytier))
$(eval $(call BuildPackage,easytier))
