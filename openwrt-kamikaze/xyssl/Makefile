# 
# Copyright (C) 2006 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.

include $(TOPDIR)/rules.mk

PKG_NAME:=xyssl
PKG_VERSION:=svn-r38
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://znerol.ch/files
PKG_MD5SUM:=ff052d1c5eb9675ce94b55c1e67752c4

include $(INCLUDE_DIR)/package.mk

define Package/xyssl/Default
  TITLE:=Embedded SSL
  URL:=http://xyssl.org/
endef

define Package/libxyssl/Default/description
 The aim of the XySSL project is to provide a quality, open-source 
 cryptographic library written in C and targeted at embedded systems.
endef

define Package/libxyssl
$(call Package/xyssl/Default)
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE+= (library)
endef

#define Package/xyssl-progs
#$(call Package/xyssl/Default)
#  SECTION:=utils
#  CATEGORY:=Utilities
#  DEPENDS:=+libxyssl
#  TITLE+= (programs)
#endef

define Build/Configure
endef

define Build/Compile
        $(MAKE) -C $(PKG_BUILD_DIR)/library \
		$(TARGET_CONFIGURE_OPTS) \
		OFLAGS="$(TARGET_CFLAGS)" \
                shared
	mkdir -p $(PKG_INSTALL_DIR)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/library/libxyssl.so $(PKG_INSTALL_DIR)/usr/lib
	mkdir -p $(PKG_INSTALL_DIR)/usr/include
	$(CP) $(PKG_BUILD_DIR)/include/xyssl $(PKG_INSTALL_DIR)/usr/include/xyssl
endef

define Build/InstallDev
	mkdir -p $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/xyssl $(1)/usr/include/
	mkdir -p $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libxyssl.so $(1)/usr/lib/
endef

define Package/libxyssl/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/lib/libxyssl.so $(1)/usr/lib/
endef

#define Package/xyssl-progs/install
#	$(INSTALL_DIR) $(1)/usr/bin
#	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/xyssl_* $(1)/usr/bin/
#endef

$(eval $(call BuildPackage,libxyssl))
#$(eval $(call BuildPackage,xyssl-progs))
