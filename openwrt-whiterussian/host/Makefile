include $(TOPDIR)/rules.mk
PKG_NAME:=host
PKG_VERSION:=20000331
PKG_RELEASE:=9
PKG_MD5SUM:=3c0bb3916025c598b3cd37b7c8e99ae1
PKG_SOURCE_URL:=http://ftp.de.debian.org/debian/pool/main/h/host
PKG_SOURCE:=$(PKG_NAME)_$(PKG_VERSION).orig.tar.gz
PKG_CAT:=zcat
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_INSTALL_DIR:=$(PKG_BUILD_DIR)/ipkg-install
include $(TOPDIR)/package/rules.mk
$(eval $(call PKG_template,HOST,$(PKG_NAME),$(PKG_VERSION)-$(PKG_RELEASE),$(ARCH)))
$(PKG_BUILD_DIR)/.configured: $(PKG_BUILD_DIR)/.prepared
	touch $@

$(PKG_BUILD_DIR)/.built:
	rm -rf $(PKG_INSTALL_DIR)
	$(MAKE) -C $(PKG_BUILD_DIR) \
		$(TARGET_CONFIGURE_OPTS) \
		CC=$(TARGET_CC) \
		LD=$(TARGET_CC) \
		CFLAGS="$(strip $(TARGET_CFLAGS))" \
		CPPFLAGS="-I$(STAGING_DIR)/usr/include" \
		LDFLAGS="-L$(STAGING_DIR)/usr/lib" \
		prefix="$(PKG_INSTALL_DIR)/usr"
	mkdir -p $(PKG_INSTALL_DIR)/usr/bin
	$(CP) $(PKG_BUILD_DIR)/host $(PKG_INSTALL_DIR)/usr/bin 
	touch $@

$(IPKG_HOST):
	install -d -m0755 $(IDIR_HOST)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/host $(IDIR_HOST)/usr/bin
	$(RSTRIP) $(IDIR_HOST)
	$(IPKG_BUILD) $(IDIR_HOST) $(PACKAGE_DIR)
mostlyclean:
	make -C $(PKG_BUILD_DIR) clean
	rm $(PKG_BUILD_DIR)/.built
