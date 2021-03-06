include $(TOPDIR)/rules.mk

PKG_NAME:=cjdns-master
PKG_VERSION:=2014-10-25-e2b673698e471dbc82b4e9dbc04cb9e16f1f06a6
PKG_RELEASE:=4

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/cjdelisle/cjdns.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=e2b673698e471dbc82b4e9dbc04cb9e16f1f06a6
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_BUILD_DEPENDS:=libssp

include $(INCLUDE_DIR)/package.mk

define Package/cjdns-master
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Routing and Redirection
  TITLE:=Experimental self configuring routing protocol.
  DEPENDS:=+kmod-tun +kmod-ipv6 +libnl +libpthread +librt +@SSP_SUPPORT +libssp
endef

define Package/cjdns-master/description
 Cjdns is a networking protocol, a system of digital rules for
 message exchange between computers. The philosophy behind cjdns
 is that networks should be easy to set up, protocols should
 scale up smoothly and security should be ubiquitous.
endef

define Build/Configure
endef

## NEON
#define Build/Compile
#	CROSS="true" \
#	CFLAGS="-O2 -march=armv7-a -mtune=cortex-a8 -mfpu=neon -ftree-vectorize -ffast-math -mfloat-abi=hard -marm -Wno-error=maybe-uninitialized" \
#	NO_PIE="true" \
#	Seccomp_NO="true" \
#	CC="$(TARGET_CC)" \
#	ARCH="$(ARCH)" \
#	LDFLAGS="$(CFLAGS) -lssp" \
#	$(PKG_BUILD_DIR)/do
#endef

# regular
define Build/Compile
	CROSS="true" \
	CFLAGS="$(TARGET_CFLAGS)" \
	NO_PIE="true" \
	Seccomp_NO="true" \
	CC="$(TARGET_CC)" \
	ARCH="$(ARCH)" \
	LDFLAGS="$(TARGET_LDFLAGS) -lssp" \
	$(PKG_BUILD_DIR)/do
endef

define Package/cjdns-master/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/cjdroute 	$(1)/usr/sbin/cjdroute
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/cjdroute 	$(1)/usr/sbin/cjdroute.master
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/privatetopublic $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/publictoip6 	$(1)/usr/sbin/

	$(INSTALL_DIR) $(1)/usr/lib/python2.7
	cp -rv $(PKG_BUILD_DIR)/contrib/python/cjdnsadmin $(1)/usr/lib/python2.7/

	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/contrib/python/cexec 	$(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/contrib/python/cjdnsa 	$(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/contrib/python/cjdnslog 	$(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/contrib/python/dumptable 	$(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/contrib/python/findnodes 	$(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/contrib/python/ip6topk 	$(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/contrib/python/peerStats 	$(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/contrib/python/pingAll.py 	$(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/contrib/python/pktoip6 	$(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/contrib/python/sessionStats 	$(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/contrib/python/trashroutes 	$(1)/usr/bin/

	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/cjdns.init $(1)/etc/init.d/cjdns
endef

$(eval $(call BuildPackage,cjdns-master))
