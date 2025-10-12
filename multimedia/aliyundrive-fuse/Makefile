include $(TOPDIR)/rules.mk

PKG_NAME:=aliyundrive-fuse
PKG_VERSION:=0.1.14
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/messense/aliyundrive-fuse/tar.gz/v$(PKG_VERSION)?
PKG_HASH:=a972342ac7e171e0b585766730c69f2e35039cb05dd987e070fcb8dbd6cf3b9f

PKG_LICENSE:=MIT
PKG_MAINTAINER:=messense <messense@icloud.com>

PKG_BUILD_DEPENDS:=rust/host

RUST_PKG_FEATURES:=rustls-tls libfuse native-tls native-tls-vendored

include $(INCLUDE_DIR)/package.mk
include ../../lang/rust/rust-package.mk

define Package/aliyundrive-fuse
  SECTION:=multimedia
  CATEGORY:=Multimedia
  DEPENDS:=+fuse-utils
  TITLE:=FUSE for AliyunDrive
  URL:=https://github.com/messense/aliyundrive-fuse
endef

define Package/aliyundrive-fuse/description
  FUSE for AliyunDrive.
endef

define Package/aliyundrive-fuse/conffiles
/etc/config/aliyundrive-fuse
endef

define Package/aliyundrive-fuse/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/target/$(RUSTC_TARGET_ARCH)/release/aliyundrive-fuse $(1)/usr/bin
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) $(CURDIR)/files/aliyundrive-fuse.init $(1)/etc/init.d/aliyundrive-fuse
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_CONF) $(CURDIR)/files/aliyundrive-fuse.config $(1)/etc/config/aliyundrive-fuse
endef

$(eval $(call BuildPackage,aliyundrive-fuse))
