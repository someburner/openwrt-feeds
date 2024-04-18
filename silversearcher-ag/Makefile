include $(TOPDIR)/rules.mk

PKG_NAME:=silversearcher-ag
PKG_VERSION:=2.2.0
PKG_RELEASE:=1
PKG_INSTALL:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/ggreer/the_silver_searcher.git
PKG_SOURCE_VERSION:=a61f1780b64266587e7bc30f0f5f71c6cca97c0f

# sha256sum of generated tar.xz
PKG_HASH:=d3fa44936b7a028808aed6644ad62924cfd8473a0a8c998bfd645934a2d7114a
# buildroot autogenerates tar.xz of missing git repos
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/silversearcher-ag
  SECTION:=utilities
  CATEGORY:=Custom Apps
  TITLE:=The Silver Searcher (ag)
  DEPENDS:=+libpthread +libpcre +liblzma +zlib
endef

define Package/silversearcher-ag/description
  A code-searching tool similar to ack, but faster.
endef

define Build/Prepare
	$(PKG_UNPACK)
	(cd $(PKG_BUILD_DIR) && ./autogen.sh)
	$(Build/Patch)
endef

define Build/Configure
 $(call Build/Configure/Default)
endef

PKG_FIXUP:=autoreconf

define Package/silversearcher-ag/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/ag $(1)/usr/bin/
endef

$(eval $(call BuildPackage,silversearcher-ag))
