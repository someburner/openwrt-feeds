#
# Copyright (C) 2017 Steven Hessing
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libtins45
PKG_VERSION:=4.5
PKG_RELEASE:=1

PKG_SOURCE:=libtins-$(PKG_VERSION).tar.gz
PKG_BUILD_DIR:=$(BUILD_DIR)/libtins-$(PKG_VERSION)
PKG_SOURCE_URL:=https://codeload.github.com/mfontanini/libtins/tar.gz/v$(PKG_VERSION)?
PKG_HASH:=6ff5fe1ada10daef8538743dccb9c9b3e19d05d028ffdc24838e62ff3fc55841

PKG_MAINTAINER:= Steven Hessing <steven.hessing@gmail.com>
PKG_LICENSE:=BSD-2-Clause
PKG_LICENSE_FILES:=LICENSE

CMAKE_INSTALL:=1
PKG_BUILD_FLAGS:=gc-sections lto

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/libtins45
  SECTION:=net
  CATEGORY:=Libraries
  TITLE:=libtins45
  URL:=https://libtins.github.io/
  DEPENDS:=+libstdcpp +LIBTINS_ENABLE_PCAP:libpcap +LIBTINS_ENABLE_WPA2:libopenssl
  MENU:=1
endef

define Package/libtins45/config
	source "$(SOURCE)/Config.in"
endef

define Package/libtins45/description
  libtins is a high-level, multiplatform C++ network packet sniffing and crafting library.
endef

CMAKE_OPTIONS += \
	-D_RUN_RESULT_VAR=FORCE \
	-DLIBTINS_BUILD_EXAMPLES=OFF \
	-DLIBTINS_BUILD_TESTS=OFF \
	-DLIBTINS_ENABLE_ACK_TRACKER=$(if $(CONFIG_LIBTINS_ENABLE_ACK_TRACKER),ON,OFF) \
	-DLIBTINS_ENABLE_CXX11=$(if $(CONFIG_LIBTINS_ENABLE_CXX11),ON,OFF) \
	-DLIBTINS_ENABLE_DOT11=$(if $(CONFIG_LIBTINS_ENABLE_DOT11),ON,OFF) \
	-DLIBTINS_ENABLE_PCAP=$(if $(CONFIG_LIBTINS_ENABLE_PCAP),ON,OFF) \
	-DLIBTINS_ENABLE_TCP_STREAM_CUSTOM_DATA=$(if $(CONFIG_LIBTINS_ENABLE_TCP_STREAM_CUSTOM_DATA),ON,OFF) \
	-DLIBTINS_ENABLE_WPA2=$(if $(CONFIG_LIBTINS_ENABLE_WPA2),ON,OFF)

TARGET_LDFLAGS += -Wl,--as-needed

define Package/libtins45/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libtins.so.* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,libtins45))
