#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=keyutils
PKG_VERSION:=1.6.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=https://people.redhat.com/dhowells/keyutils/
PKG_HASH:=c8b15722ae51d95b9ad76cc6d49a4c2cc19b0c60f72f61fb9bf43eea7cbd64ce

PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

define Package/libkeyutils
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=Key utilities library
  URL:=https://people.redhat.com/dhowells/keyutils/
  LICENSE:=LGPL-2.1-or-later
  LICENSE_FILES:=LICENSE.LGPL
  ABI_VERSION:=1
endef

define Package/keyctl
  SECTION:=utils
  CATEGORY:=Utilities
  SUBMENU:=Encryption
  TITLE:=keyctl
  DEPENDS:=+libkeyutils
  LICENSE:=GPL-2.0-or-later
  LICENSE_FILES:=LICENSE.GPL
endef

define Package/keyutils/description
  Key utilities
endef

MAKE_FLAGS += \
	BINDIR=/usr/bin \
	LIBDIR=/usr/lib \
	SBINDIR=/usr/sbin \
	CFLAGS="$(TARGET_CFLAGS) $(FPIC)"

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/* $(1)/usr/include/
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libkeyutils.a $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libkeyutils.so.$(ABI_VERSION)* $(1)/usr/lib/
endef

define Package/libkeyutils/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libkeyutils.so.$(ABI_VERSION)* $(1)/usr/lib/
endef

define Package/keyctl/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/keyctl $(1)/usr/bin
endef

$(eval $(call BuildPackage,libkeyutils))
$(eval $(call BuildPackage,keyctl))
