# 
# Copyright (C) 2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=distrotech-foomatic-filters
PKG_VERSION:=4.0.17
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/Distrotech/foomatic-filters/archive
PKG_MD5SUM:=1feef3c5d09cbccbee9bb313924ef564

PKG_BUILD_DEPENDS:=cups

include $(INCLUDE_DIR)/package.mk

define Package/distrotech-foomatic-filters
  SECTION:=net
  CATEGORY:=Network
  TITLE:=Foomatic filters for CUPS
  URL:=https://github.com/Distrotech/foomatic-filters/
  DEPENDS:=cups
  SUBMENU:=Printing
endef

define Package/distrotech-foomatic-filters/description
Filter scripts used by the printer spoolers to convert the incoming
PostScript data into the printer's native format using a
printer/driver specific, but spooler-independent PPD file.
endef

define Build/Prepare
	echo $(DL_DIR) > /home/joshiu/Documents/dldir.txt
	echo $(PKG_BUILD_DIR) >> /home/joshiu/Documents/dldir.txt
	mkdir -p $(PKG_BUILD_DIR)
	tar -zxf $(DL_DIR)/$(PKG_SOURCE) -C $(PKG_BUILD_DIR)
	cp -r $(PKG_BUILD_DIR)/foomatic-filters*/* $(PKG_BUILD_DIR)
	rm -rf $(PKG_BUILD_DIR)/foomatic-filters*
	cd $(PKG_BUILD_DIR) && ./make_configure
endef

define Build/Configure
	$(call Build/Configure/Default, \
		--disable-dbus \
		UNAME="Linux" \
		LIBS="-Wl,-rpath-link=$(STAGING_DIR)/usr/lib" \
	)
endef

define Package/distrotech-foomatic-filters/install
	$(INSTALL_DIR) $(1)/usr/lib/cups/filter
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/lib/cups/filter/foomatic-rip $(1)/usr/lib/cups/filter/
	$(INSTALL_DIR) $(1)/usr/lib/cups/backend
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/lib/cups/backend/beh $(1)/usr/lib/cups/backend/
endef


$(eval $(call BuildPackage,distrotech-foomatic-filters))
