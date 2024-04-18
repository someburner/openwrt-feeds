include $(TOPDIR)/rules.mk

PKG_NAME:=mqtt-dissector
PKG_VERSION:=1.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/someburner/mqtt-dissector.git
PKG_SOURCE_VERSION:=139e6b38f3509ce936284935c2b9d937b0633705

# sha256sum of generated tar.xz
PKG_HASH:=aa39791af47bdd3f8ad759c659f9f92f818a45dcf4afef4daefca5a730e7706f
# buildroot autogenerates tar.xz of missing git repos
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

TARGET_CFLAGS += -DLOGURU_EN=0 -DEN_DEVMODE=1
TARGET_CXXFLAGS += -DLOGURU_EN=0 -DEN_DEVMODE=1
TARGET_CXXFLAGS += -pedantic -O2 -std=c++17 -D_REETRANT -pthread
TARGET_LDFLAGS += -lpcap -lstdc++ -ltins

define Package/mqtt-dissector
  SECTION:=net
  CATEGORY:=Custom Apps
  TITLE:=mqtt-dissector
  DEPENDS:=+libstdcpp +libpcap +libtins
  PKG_BUILD_DEPENDS:=libpcap libtins boost
endef

define Package/mqtt-dissector/description
  Leverage libpcap and libtins to decode MQTT messages on an interface.
endef

define Build/Prepare
	$(PKG_UNPACK)
	(cd $(PKG_BUILD_DIR) && cp config.example.mk config.mk;)
	$(Build/Patch)
endef

define Build/Compile
	$(TARGET_CXX) $(TARGET_CXXFLAGS) -o $(PKG_BUILD_DIR)/main.o -c $(PKG_BUILD_DIR)/src/main.cpp
	$(TARGET_CXX) $(TARGET_CXXFLAGS) -o $(PKG_BUILD_DIR)/dissect.o -c $(PKG_BUILD_DIR)/src/dissect.cpp
	$(TARGET_CXX) -o $(PKG_BUILD_DIR)/$1 $(PKG_BUILD_DIR)/main.o $(PKG_BUILD_DIR)/dissect.o $(TARGET_LDFLAGS)
endef

define Package/mqtt-dissector/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/mqtt-dissector $(1)/usr/bin
endef

# This command is always the last, it uses the definitions and variables we give above in order to get the job done
$(eval $(call BuildPackage,mqtt-dissector))
