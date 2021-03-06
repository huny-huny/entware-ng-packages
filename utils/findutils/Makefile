#
# Copyright (C) 2006-2016 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
include $(TOPDIR)/rules.mk

PKG_NAME:=findutils
PKG_VERSION:=4.6.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@GNU/$(PKG_NAME)
PKG_HASH:=ded4c9f73731cd48fec3b6bdaccce896473b6d8e337e9612e16cf1431bb1169d
PKG_MAINTAINER:=Daniel Dickinson <lede@daniel.thecshore.com>

PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/findutils/Default
	TITLE:=GNU findutils
	SECTION:=utils
	CATEGORY:=Utilities
endef

define Package/findutils/description/Default
Replace busybox versions of findutils with full GNU versions.
This is normally not needed as busybox is smaller and provides
sufficient functionality, but some users may want or need
the full functionality of the GNU tools.
endef

define Package/findutils
	$(call Package/findutils/Default)
endef


define Package/findutils/description
$(call Package/findutils/description/Default)
This package installs find and xargs utilities
endef



define Package/findutils-locate
	$(call Package/findutils/Default)
	TITLE := (locate)
endef

define Package/findutils-locate/description
$(call Package/findutils/description/Default)
This package contains the locate and related updatedb utility
endef

CONFIGURE_ARGS += --localstatedir=/opt/var
CONFIGURE_VARS += ac_cv_path_SORT=sort

define Package/findutils/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/{find,xargs} \
	    $(1)/opt/bin/
endef

define Package/findutils-locate/install
	$(INSTALL_DIR) $(1)/opt/bin $(1)/opt/var
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/locate $(1)/opt/bin/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/updatedb $(1)/opt/bin/
	$(CP) $(PKG_INSTALL_DIR)/opt/lib $(1)/opt/
endef

$(eval $(call BuildPackage,findutils))
$(eval $(call BuildPackage,findutils-locate))
