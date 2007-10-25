include $(TOPDIR)/rules.mk
PKG_NAME:=xyssl
PKG_VERSION:=0.8
PKG_RELEASE:=1
PKG_MD5SUM:=5c80e021e3bca4b77fbe2429c9e61541
PKG_SOURCE_URL:=http://www.xyssl.org/code/download
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tgz
PKG_CAT:=zcat
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_INSTALL_DIR:=$(PKG_BUILD_DIR)/ipkg-install
include $(TOPDIR)/package/rules.mk
$(eval $(call PKG_template,XYSSL,$(PKG_NAME),$(PKG_VERSION)-$(PKG_RELEASE),$(ARCH)))
$(PKG_BUILD_DIR)/.configured: $(PKG_BUILD_DIR)/.prepared
	touch $@

$(PKG_BUILD_DIR)/.built:
	rm -rf $(PKG_INSTALL_DIR)
	$(MAKE) -C $(PKG_BUILD_DIR)/library \
		CC=$(TARGET_CC) \
		$(TARGET_CONFIGURE_OPTS) \
		prefix="$(PKG_INSTALL_DIR)/usr" \
		shared
	mkdir -p $(PKG_INSTALL_DIR)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/library/libxyssl.so $(PKG_INSTALL_DIR)/usr/lib 
	touch $@

$(IPKG_XYSSL):
	install -d -m0755 $(IDIR_XYSSL)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libxyssl.so $(IDIR_XYSSL)/usr/lib
	$(RSTRIP) $(IDIR_XYSSL)
	$(IPKG_BUILD) $(IDIR_XYSSL) $(PACKAGE_DIR)

$(STAGING_DIR)/usr/lib/libxyssl.so: $(PKG_BUILD_DIR)/.built
	mkdir -p $(STAGING_DIR)/usr/include
	$(CP) -r $(PKG_BUILD_DIR)/include/xyssl $(STAGING_DIR)/usr/include
	mkdir -p $(STAGING_DIR)/usr/lib/
	$(CP) $(PKG_BUILD_DIR)/library/libxyssl.so $(STAGING_DIR)/usr/lib/
	touch $@

install-dev: $(STAGING_DIR)/usr/lib/libxyssl.so

uninstall-dev:
	rm -rf \
		$(STAGING_DIR)/usr/include/xyssl
		$(STAGING_DIR)/usr/lib/libxyssl.so

compile: install-dev
clean: uninstall-dev

mostlyclean:
	make -C $(PKG_BUILD_DIR) clean
	rm $(PKG_BUILD_DIR)/.built
