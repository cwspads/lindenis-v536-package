#
# Copyright (C) 2006-2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=vala
PKG_VERSION:=0.34.2
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=@GNOME/vala/0.34/
#PKG_MD5SUM:=84b742e9cca4c90fde3026c3793c03c1

PKG_BUILD_DEPENDS:=glib2/host vala/host
HOST_BUILD_DEPENDS:=glib2/host

include $(BUILD_DIR)/host-build.mk
include $(BUILD_DIR)/package.mk
include $(BUILD_DIR)/nls.mk

TARGET_LDFLAGS+=\
	-Wl,-rpath-link=$(STAGING_DIR)/usr/lib

define Package/vala
	SECTION:=lang
	CATEGORY:=Languages
	TITLE:=C-sharp like language for the GObject system
	URL:=http://live.gnome.org/Vala
endef

define Package/vala/description
Vala is a C-sharp like language for the GObject system. This package contains
the Vala-to-C compiler.
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
	DESTDIR="$(PKG_INSTALL_DIR)" \
	all install
endef

define Host/Install
	rm -f $(STAGING_DIR_HOSTPKG)/bin/rake
	$(call Host/Install/Default)
	$(INSTALL_BIN) $(STAGING_DIR)/host/bin/* $(STAGING_DIR_HOST)/bin/
endef

define Build/InstallDev
	$(INSTALL_DIR) \
	$(1)/usr/share/vala-0.34/vapi \
	$(1)/usr/lib \
	$(1)/usr/share/pkgconfig \
	$(1)/usr/bin

	$(INSTALL_DATA) \
	$(PKG_INSTALL_DIR)/usr/share/vala-0.34/vapi/* \
	$(1)/usr/share/vala-0.34/vapi

	$(INSTALL_DATA) \
	$(PKG_INSTALL_DIR)/usr/lib/libvala-0.34.{so*,la} \
	$(1)/usr/lib

	$(INSTALL_BIN) \
	$(PKG_INSTALL_DIR)/usr/bin/{vala,vala-0.34,valac,valac-0.34,vapicheck,vapicheck-0.34,vapigen,vapigen-0.34,vala-gen-introspect,vala-gen-introspect-0.34} \
	$(1)/usr/bin

endef

$(eval $(call HostBuild))
$(eval $(call BuildPackage,vala))
