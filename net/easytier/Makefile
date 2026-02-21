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

include $(INCLUDE_DIR)/package.mk
include ../../lang/rust/rust-package.mk

define Package/easytier
	SECTION:=net
	CATEGORY:=Network
	TITLE:=A simple, decentralized mesh VPN with WireGuard support.
	DEPENDS:=@(x86_64||arm||aarch64||mipsel||mips) +kmod-tun
	URL:=https://github.com/EasyTier/EasyTier
endef

define Package/easytier/description
  A simple, decentralized mesh VPN with WireGuard support.
endef

define Build/Compile
	$(call Build/Compile/Cargo,easytier)
endef

$(eval $(call RustBinPackage,easytier))
$(eval $(call BuildPackage,easytier))
