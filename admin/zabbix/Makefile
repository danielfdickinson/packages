#
# Copyright (C) 2006-2015 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=zabbix
PKG_VERSION:=7.0.22
PKG_RELEASE:=3

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://cdn.zabbix.com/zabbix/sources/stable/$(basename $(PKG_VERSION))/ \
	https://cdn.zabbix.com/zabbix/sources/oldstable/$(basename $(PKG_VERSION))/
PKG_HASH:=7a74794b2124607d8036be36cc104da056a2fb653811c84acbe29f3f6d97860a

PKG_MAINTAINER:=Daniel F. Dickinson <dfdpublic@wildtechgarden.ca>
PKG_LICENSE:=AGPL-3.0-only
PKG_LICENSE_FILES:=COPYING
PKG_CPE_ID:=cpe:/a:zabbix:zabbix

PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/zabbix/Default
  SECTION:=admin
  CATEGORY:=Administration
  SUBMENU:=Zabbix
  TITLE:=Zabbix
  URL:=https://www.zabbix.com/
endef

define Package/zabbix-agentd/Default
  $(call Package/zabbix/Default)
  TITLE+= agentd
  DEPENDS:= \
    $(ICONV_DEPENDS) \
    +libevent2-pthreads \
    +libpcre2 \
    +zlib
  PROVIDES:=zabbix-agentd
  USERID:=zabbix-agent=53:zabbix-agent=53
endef

define Package/zabbix-agentd-tiny
  $(call Package/zabbix-agentd/Default)
  TITLE+= (core/no SSL)
  PROVIDES+= zabbix-agentd-nossl
  VARIANT:=tiny
  DEFAULT_VARIANT:=1
endef

define Package/zabbix-agentd-openssl
  $(call Package/zabbix-agentd/Default)
  TITLE+= (core/with OpenSSL)
  DEPENDS+= +libopenssl
  PROVIDES+= zabbix-agentd-ssl
  VARIANT:=openssl
endef

define Package/zabbix-agentd-gnutls
  $(call Package/zabbix-agentd/Default)
  TITLE+= (core/with GnuTLS)
  DEPENDS+= +libgnutls
  PROVIDES+= zabbix-agentd-ssl
  VARIANT:=gnutls
endef

define Package/zabbix-agentd-full
  $(call Package/zabbix-agentd/Default)
  TITLE+= (full/with OpenSSL)
  DEPENDS:= \
    +libnetsnmp-ssl \
    +libopenldap \
    +libopenssl
  PROVIDES+= zabbix-agentd-ssl
  VARIANT:=full
endef

define Package/zabbix-agentd-curl-gnutls
  $(call Package/zabbix-agentd/Default)
  TITLE+= (cURL/with GnuTLS)
  DEPENDS+= \
    +libcurl-gnutls \
    +libgnutls
  PROVIDES+= zabbix-agentd-ssl
  VARIANT:=curl-gnutls
endef

define Package/zabbix-sender/Default
  $(call Package/zabbix/Default)
  TITLE+= sender
  DEPENDS:= \
    $(ICONV_DEPENDS) \
    +libpcre2 \
    +zlib
  PROVIDES:=zabbix-sender
endef

define Package/zabbix-sender-tiny
  $(call Package/zabbix-sender/Default)
  TITLE+= (core/no SSL)
  PROVIDES+= zabbix-sender-nossl
  VARIANT:=tiny
  DEFAULT_VARIANT:=1
endef

define Package/zabbix-sender-openssl
  $(call Package/zabbix-sender/Default)
  TITLE+= (core/with OpenSSL)
  DEPENDS+= +libopenssl
  PROVIDES+= zabbix-sender-ssl
  VARIANT:=openssl
endef

define Package/zabbix-sender-gnutls
  $(call Package/zabbix-sender/Default)
  TITLE+= (core/with GnuTLS)
  DEPENDS+= +libgnutls
  PROVIDES+= zabbix-sender-ssl
  VARIANT:=gnutls
endef

define Package/zabbix-get/Default
  $(call Package/zabbix/Default)
  TITLE+= get
  DEPENDS:= \
    $(ICONV_DEPENDS) \
    +libpcre2 \
    +zlib
  PROVIDES:=zabbix-get
endef

define Package/zabbix-get-tiny
  $(call Package/zabbix-get/Default)
  TITLE+= (core/no SSL)
  PROVIDES+= zabbix-get-nossl
  VARIANT:=tiny
  DEFAULT_VARIANT:=1
endef

define Package/zabbix-get-openssl
  $(call Package/zabbix-get/Default)
  TITLE+= (core/with OpenSSL)
  DEPENDS+= +libopenssl
  PROVIDES+= zabbix-get-ssl
  VARIANT:=openssl
endef

define Package/zabbix-get-gnutls
  $(call Package/zabbix-get/Default)
  TITLE+= (core/with GnuTLS)
  DEPENDS+= +libgnutls
  PROVIDES+= zabbix-get-ssl
  VARIANT:=gnutls
endef

define Package/zabbix-server-or-proxy/Default
  $(call Package/zabbix/Default)
  DEPENDS:= \
    $(ICONV_DEPENDS) \
    +fping \
    +libevent2 \
    +libevent2-pthreads \
    +libevent2-extra \
    +libpcre2 \
    +zlib
  USERID:=zabbix-server=70:zabbix-server=70
endef

define Package/zabbix-server-postgresql/Default
  $(call Package/zabbix-server-or-proxy/Default)
  TITLE+= server postgresql
  DEPENDS+= +libpq
  PROVIDES:=\
    zabbix-server \
    zabbix-server-postgresql
endef

define Package/zabbix-server-small-postgresql
  $(call Package/zabbix-server-postgresql/Default)
  TITLE+= (core/no SSL)
  PROVIDES+= \
    zabbix-server-nossl \
    zabbix-server-nossl-postgresql \
    zabbix-server-small
  VARIANT:=small
  DEFAULT_VARIANT:=1
endef

define Package/zabbix-server-openssl-postgresql
  $(call Package/zabbix-server-postgresql/Default)
  TITLE+= (core/with OpenSSL)
  DEPENDS+= +libopenssl
  PROVIDES+= \
    zabbix-server-openssl \
    zabbix-server-ssl \
    zabbix-server-ssl-postgresql
  VARIANT:=openssl
endef

define Package/zabbix-server-gnutls-postgresql
  $(call Package/zabbix-server-postgresql/Default)
  TITLE+= (core/with GnuTLS)
  DEPENDS+= +libgnutls
  PROVIDES+= \
    zabbix-server-gnutls \
    zabbix-server-ssl \
    zabbix-server-ssl-postgresql
  VARIANT:=gnutls
endef

define Package/zabbix-server-full-postgresql
	$(call Package/zabbix-server-postgresql/Default)
  TITLE+= (full/with OpenSSL)
  DEPENDS+= \
    +libcurl \
    +libnetsnmp-ssl \
    +libopenldap \
    +libopenssl
  PROVIDES+= \
    zabbix-server-full \
    zabbix-server-openssl \
    zabbix-server-ssl \
    zabbix-server-ssl-postgresql
  VARIANT:=full
endef

define Package/zabbix-server-curl-gnutls-postgresql
  $(call Package/zabbix-server-postgresql/Default)
  TITLE+= (core/with GnuTLS)
  DEPENDS+= \
    +libcurl-gnutls \
    +libgnutls
  PROVIDES+= \
    zabbix-server-curl-gnutls \
    zabbix-server-gnutls \
    zabbix-server-ssl \
    zabbix-server-ssl-postgresql
  VARIANT:=gnutls-curl
endef

define Package/zabbix-server-mariadb/Default
	$(call Package/zabbix-server-or-proxy/Default)
  TITLE+= server mariadb
  DEPENDS+= +libmariadbclient
  PROVIDES:= \
    zabbix-server \
    zabbix-server-mariadb
endef

define Package/zabbix-server-small-mariadb
  $(call Package/zabbix-server-mariadb/Default)
  TITLE+= (core/no SSL)
  PROVIDES+= \
    zabbix-server-nossl \
    zabbix-server-nossl-mariadb \
    zabbix-server-small
  VARIANT:=small-mariadb
  DEFAULT_VARIANT:=1
endef

define Package/zabbix-server-openssl-mariadb
	$(call Package/zabbix-server-mariadb/Default)
  TITLE+= (with OpenSSL)
  DEPENDS+= +libopenssl
  PROVIDES+= \
    zabbix-server-openssl \
    zabbix-server-ssl \
    zabbix-server-ssl-mariadb
  VARIANT:=openssl-mariadb
endef

define Package/zabbix-server-gnutls-mariadb
	$(call Package/zabbix-server-mariadb/Default)
  TITLE+= (with GnuTLS)
  DEPENDS+= +libgnutls
  PROVIDES+= \
    zabbix-server-gnutls \
    zabbix-server-ssl \
    zabbix-server-ssl-mariadb
  VARIANT:=gnutls-mariadb
endef

define Package/zabbix-server-full-mariadb
	$(call Package/zabbix-server-mariadb/Default)
  TITLE+= (full/with OpenSSL)
  DEPENDS+= \
    +libcurl \
    +libnetsnmp-ssl \
    +libopenldap \
    +libopenssl
  PROVIDES+= \
    zabbix-server-full \
    zabbix-server-openssl \
    zabbix-server-ssl \
    zabbix-server-ssl-mariadb
  VARIANT:=full-mariadb
endef

define Package/zabbix-server-curl-gnutls-mariadb
	$(call Package/zabbix-server-mariadb/Default)
  TITLE+= (cURL/with GnuTLS)
  DEPENDS+= \
    +libcurl-gnutls \
    +libgnutls
  PROVIDES+= \
    zabbix-server-curl-gnutls \
    zabbix-server-gnutls \
    zabbix-server-ssl \
    zabbix-server-mariadb-ssl
  VARIANT:=curl-mariadb
endef

define Package/zabbix-proxy/Default
  $(call Package/zabbix-server-or-proxy/Default)
  TITLE+= proxy
  PROVIDES:=zabbix-proxy
endef

define Package/zabbix-proxy-tiny
	$(call Package/zabbix-proxy/Default)
  TITLE+= sqlite3 (core/no SSL)
  DEPENDS += +libsqlite3
  PROVIDES+= \
    zabbix-proxy-nossl \
    zabbix-proxy-sqlite
  VARIANT:=tiny
  DEFAULT_VARIANT:=1
endef

define Package/zabbix-proxy-postgresql/Default
	$(call Package/zabbix-proxy/Default)
  TITLE+= postgresql
  DEPENDS+= +libpq
  PROVIDES+= zabbix-proxy-postgresql
endef

define Package/zabbix-proxy-small-postgresql
  $(call Package/zabbix-proxy-postgresql/Default)
  TITLE+= (core/no SSL)
  PROVIDES+= \
    zabbix-proxy-small \
    zabbix-proxy-nossl \
    zabbix-proxy-nossl-postgresql
  VARIANT:=small
endef

define Package/zabbix-proxy-openssl-postgresql
  $(call Package/zabbix-proxy-postgresql/Default)
  TITLE+= (core/with OpenSSL)
  DEPENDS+= +libopenssl
  PROVIDES+= \
    zabbix-proxy-openssl \
    zabbix-proxy-ssl
  VARIANT:=openssl
endef

define Package/zabbix-proxy-gnutls-postgresql
  $(call Package/zabbix-proxy-postgresql/Default)
  TITLE+= (core/with GnuTLS)
  DEPENDS+= +libgnutls
  PROVIDES+= \
    zabbix_proxy-gnutls \
    zabbix-proxy-ssl
  VARIANT:=gnutls
endef

define Package/zabbix-proxy-full-postgresql
	$(call Package/zabbix-proxy-postgresql/Default)
  TITLE+= (full/with OpenSSL)
  DEPENDS+= \
    +libcurl \
    +libnetsnmp-ssl \
    +libopenldap \
    +libopenssl
  PROVIDES+= \
    zabbix-proxy-full \
    zabbix-proxy-openssl \
    zabbix-proxy-ssl
  VARIANT:=full
endef

define Package/zabbix-proxy-curl-gnutls-postgresql
	$(call Package/zabbix-proxy-postgresql/Default)
  TITLE+= (cURL/with GnuTLS)
  DEPENDS+= \
    +libcurl-gnutls \
    +libgnutls
  PROVIDES+= \
    zabbix-proxy-curl-gnutls \
    zabbix-proxy-gnutls \
    zabbix-proxy-postgresql \
    zabbix-proxy-ssl
  VARIANT:=curl-gnutls
endef

define Package/zabbix-proxy-mariadb/Default
	$(call Package/zabbix-proxy/Default)
  TITLE+= mariadb
  DEPENDS+= +libmariadbclient
  PROVIDES+= zabbix-proxy-mariadb
endef

define Package/zabbix-proxy-small-mariadb
  $(call Package/zabbix-proxy-mariadb/Default)
  TITLE+= (core/no SSL)
  PROVIDES+= \
    zabbix-proxy-nossl \
    zabbix-proxy-nossl-mariadb \
    zabbix-proxy-small
  VARIANT:=small-mariadb
endef

define Package/zabbix-proxy-openssl-mariadb
	$(call Package/zabbix-proxy-mariadb/Default)
  TITLE+= (core/with OpenSSL)
  DEPENDS+= +libopenssl
  PROVIDES+= \
    zabbix-proxy-ssl \
    zabbix-proxy-openssl
  VARIANT:=openssl-mariadb
endef

define Package/zabbix-proxy-gnutls-mariadb
	$(call Package/zabbix-proxy-mariadb/Default)
  TITLE+= (core/with GnuTLS)
  DEPENDS+= +libgnutls
  PROVIDES+= \
    zabbix-proxy-gnutls \
    zabbix-proxy-ssl
  VARIANT:=gnutls-mariadb
endef

define Package/zabbix-proxy-full-mariadb
	$(call Package/zabbix-proxy-mariadb/Default)
  TITLE+= (full/with OpenSSL)
  DEPENDS+= \
    +libcurl \
    +libnetsnmp-ssl \
    +libopenldap \
    +libopenssl
  PROVIDES+= \
    zabbix-proxy-full \
    zabbix-proxy-mariadb \
    zabbix-proxy-openssl \
    zabbix-proxy-ssl
  VARIANT:=full-mariadb
endef

define Package/zabbix-proxy-curl-gnutls-mariadb
	$(call Package/zabbix-proxy-mariadb/Default)
  TITLE+= (cURL/with GnuTLS)
  DEPENDS+= \
    +libcurl-gnutls \
    +libgnutls
  PROVIDES+= \
    zabbix-proxy-curl-gnutls \
    zabbix-proxy-gnutls \
    zabbix-proxy-ssl
  VARIANT:=curl-mariadb
endef

define Package/zabbix-extra-mac80211
  $(call Package/zabbix/Default)
  TITLE+= discovery/userparameters for mac80211
  DEPENDS:= \
    @KERNEL_DEBUG_FS \
    @PACKAGE_MAC80211_DEBUGFS \
    +zabbix-agentd
  VARIANT:=no-configure
endef

define Package/zabbix-extra-network
  $(call Package/zabbix/Default)
  TITLE+= discovery/userparameters for network
  DEPENDS:= \
    +libubus-lua \
    +lua \
    +zabbix-agentd
  VARIANT:=no-configure
endef

define Package/zabbix-extra-wifi
  $(call Package/zabbix/Default)
  TITLE+= discovery/userparameters for wifi
  DEPENDS:= \
    +libiwinfo-lua \
    +libubus-lua +lua \
    +zabbix-agentd
  VARIANT:=no-configure
endef

define Package/zabbix-frontend-server/Default
  $(call Package/zabbix/Default)
  TITLE+= frontend server
  DEPENDS:= \
    @PACKAGE_php8 \
    +php8-cgi \
    +php8-mod-gd \
    +php8-mod-bcmath \
    +php8-mod-ctype \
    +php8-mod-filter \
    +php8-mod-gettext \
    +php8-mod-mbstring \
    +php8-mod-openssl \
    +php8-mod-session \
    +php8-mod-sockets \
    +php8-mod-xmlreader \
    +php8-mod-xmlwriter
  PROVIDES:=\
    zabbix-frontend-server \
    zabbix-server-frontend
endef

define Package/zabbix-frontend-server-postgresql
  $(call Package/zabbix-frontend-server/Default)
  TITLE+= postgresql
  DEPENDS+= +php8-mod-pgsql
  VARIANT:=no-configure
endef

define Package/zabbix-frontend-server-mariadb
	$(call Package/zabbix-frontend-server/Default)
  TITLE+= mariadb
  DEPENDS+= +php8-mod-mysqli
  VARIANT:=no-configure-mariadb
endef

define Package/zabbix-frontend-server-extra-auth-postgresql
	$(call Package/zabbix-frontend-server/Default)
  TITLE+= postgresql
  DEPENDS+= \
    +php8-mod-curl \
    +php8-mod-ldap \
    +php8-mod-pgsql
  PROVIDES+= zabbix-frontend-server-extra-auth
  VARIANT:=no-configure-extra-auth
endef

define Package/zabbix-frontend-server-extra-auth-mariadb
	$(call Package/zabbix-frontend-server/Default)
  TITLE+= mariadb
  DEPENDS+= \
    +php8-mod-curl \
    +php8-mod-ldap \
    +php8-mod-mysqli
  PROVIDES+= zabbix-frontend-server-extra-auth
  VARIANT:=no-configure-extra-auth-mariadb
endef

define Package/zabbix-extra-mac80211/description
An extra package for zabbix-agentd that adds a discovery rule for mac80211 wifi phy and many userparameters.
It contains an suid helper to allow zabbix-agentd to still run as zabbix user and not as root.
See https://openwrt.org/docs/guide-user/services/network_monitoring/zabbix for ready to use zabbix templates.
endef

define Package/zabbix-extra-network/description
An extra package for zabbix-agentd that adds a discovery rule for openwrt network interfaces.
The idea here is to discover only interfaces listed in /etc/config/network (discover br-lan and not eth0.1 and wlan0)
See https://openwrt.org/docs/guide-user/services/network_monitoring/zabbix for ready to use zabbix templates.
endef

define Package/zabbix-extra-wifi/description
An extra package for zabbix-agentd that adds a discovery rule for wifi interfaces and many userparameters.
As it uses libiwinfo, it works with all wifi devices supported by openwrt.
See https://openwrt.org/docs/guide-user/services/network_monitoring/zabbix for ready to use zabbix templates.
endef

ifeq ($(filter no-configure no-configure-mariadb no-configure-extra-auth no-configure-extra-auth-mariadb,$(BUILD_VARIANT)),)

CONFIGURE_ARGS+= \
	$(call autoconf_bool,CONFIG_IPV6,ipv6) \
  --disable-java \
  --with-libevent=$(STAGING_DIR)/usr/include \
  --with-libpcre2=$(STAGING_DIR)/usr/include \
  --with-zlib=$(STAGING_DIR)/usr/include

ifeq ($(BUILD_VARIANT),tiny)
CONFIGURE_ARGS+= --with-sqlite3=$(STAGING_DIR)/usr \
  --enable-agent --disable-server --enable-proxy
endif

ifneq ($(filter openssl gnutls full curl-gnutls,$(BUILD_VARIANT)),)
CONFIGURE_ARGS+= --enable-agent --enable-server --enable-proxy
endif

ifneq ($(filter small small-mariadb openssl-mariadb gnutls-mariadb full-mariadb curl-mariadb,$(BUILD_VARIANT)),)
CONFIGURE_ARGS+= --disable-agent --enable-server --enable-proxy
endif

ifneq ($(filter small openssl gnutls full curl-gnutls,$(BUILD_VARIANT)),)
CONFIGURE_ARGS+= --with-postgresql
endif

ifneq ($(filter small-mariadb openssl-mariadb gnutls-mariadb full-mariadb curl-mariadb,$(BUILD_VARIANT)),)
CONFIGURE_ARGS+= --with-mysql
endif

ifneq ($(filter tiny small small-mariadb,$(BUILD_VARIANT)),)
CONFIGURE_ARGS+= --with-openssl="no" --with-gnutls="no"
endif

ifneq ($(filter openssl openssl-mariadb full full-mariadb,$(BUILD_VARIANT)),)
CONFIGURE_ARGS+= --with-openssl="$(STAGING_DIR)/usr"
endif

ifneq ($(filter gnutls gnutls-mariadb curl-gnutls curl-gnutls-mariadb,$(BUILD_VARIANT)),)
CONFIGURE_ARGS+= --with-gnutls="$(STAGING_DIR)/usr"
endif

ifneq ($(filter full full-mariadb,$(BUILD_VARIANT)),)
CONFIGURE_ARGS += --with-ldap="$(STAGING_DIR)/usr"
CONFIGURE_ARGS += --with-libcurl
CONFIGURE_ARGS += \
  ac_cv_path__libnetsnmp_config_bin="$(STAGING_DIR)/host/bin" \
  ac_cv_path__libnetsnmp_config_root="$(STAGING_DIR)/host/bin/net-snmp-config"
CONFIGURE_ARGS += --with-net-snmp
endif

ifneq ($(filter curl curl-mariadb,$(BUILD_VARIANT)),)
CONFIGURE_VARS += \
  LIBCURL_LIBS="-lcurl-gnutls" \
  LIBCURL_CPPFLAGS="-I$(STAGING_DIR)/usr/include" \
  LIBCURL_LDFLAGS="-L$(STAGING_DIR)/usr/lib" \
  libcurl_cv_lib_curl_version=8.14.1 \
  ac_cv_path__libcurl_config="/bin/true" \
  libcurl_cv_lib_curl_usable=yes \
  libcurl_cv_lib_curl_version_ok=yes
CONFIGURE_ARGS += --with-libcurl="yes"
endif

else

define Build/Prepare
	true
endef
define Build/Configure
	true
endef
define Build/Compile
	true
endef

endif

ifdef CONFIG_PACKAGE_zabbix-extra-mac80211

define Build/Prepare
	$(call Build/Prepare/Default)
	mkdir -p $(PKG_BUILD_DIR)/zabbix-extra-mac80211
	$(CP) ./files/zabbix_helper_mac80211.c $(PKG_BUILD_DIR)/zabbix-extra-mac80211/
endef

define Build/Configure
	$(call Build/Configure/Default)
endef

# We use spaces for continued lines so that is if continuation does not parse
# properly we will get a hard error instead of subtle failure.
define Build/Compile
	$(call Build/Compile/Default)
	$(TARGET_CC) $(TARGET_CFLAGS) \
    $(PKG_BUILD_DIR)/zabbix-extra-mac80211/zabbix_helper_mac80211.c \
    -o $(PKG_BUILD_DIR)/zabbix-extra-mac80211/zabbix_helper_mac80211
endef

endif

MAKE_FLAGS += ARCH="linux"

define Package/zabbix/install/sbin
	$(INSTALL_DIR) \
		$(1)/usr/sbin

	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/usr/sbin/zabbix_$(2) \
		$(1)/usr/sbin/
endef

define Package/zabbix/install/bin
	$(INSTALL_DIR) \
		$(1)/usr/bin

	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/usr/bin/zabbix_$(2) \
		$(1)/usr/bin/
endef

define Package/zabbix/install/etc
	$(INSTALL_DIR) \
		$(1)/etc

	$(INSTALL_CONF) \
		$(PKG_INSTALL_DIR)/etc/zabbix_$(2).conf \
		$(1)/etc/
endef

define Package/zabbix/install/init.d
	$(INSTALL_DIR) \
		$(1)/etc/init.d

	$(INSTALL_BIN) \
		./files/zabbix_$(2).init \
		$(1)/etc/init.d/zabbix_$(2)
endef

define Package/zabbix/install/zabbix.conf.d
	$(INSTALL_DIR) \
		$(1)/etc/zabbix_agentd.conf.d

	$(INSTALL_BIN) \
		./files/$(2) \
		$(1)/etc/zabbix_agentd.conf.d/$(2)
endef

# Due to nested defines, eval, and call, the extra spaces for the nested define,
# and tabs for the part that actually executes in a shell, is essential.
define Package/zabbix-daemon/files
        define Package/zabbix-$(1)-$(2)/conffiles
  /etc/zabbix_$(1).conf
  $(3)
        endef
        define Package/zabbix-$(1)-$(2)/install
		$(INSTALL_DIR) $$(1)/etc/zabbix_$(1).conf.d
		$(call Package/zabbix/install/sbin,$$(1),$(1))
		$(4)
        endef
endef

define Package/zabbix-server/conffiles-extra
/etc/config/zabbix_server
/etc/sysctl.d/90-zabbix-discovery-workers.conf
endef

define Package/zabbix-agentd/install-extra
	$(call Package/zabbix/install/etc,$$(1),agentd)
	$(call Package/zabbix/install/init.d,$$(1),agentd)
endef

define Package/zabbix-server/install-extra
	$(call Package/zabbix/install/etc,$$(1),server)
	$(call Package/zabbix/install/init.d,$$(1),server)
	$(INSTALL_DIR) $$(1)/etc/sysctl.d
	$(INSTALL_CONF) ./files/zabbix-discovery-workers.conf.sysctl \
    $$(1)/etc/sysctl.d/90-zabbix-discovery-workers.conf
	$(INSTALL_DIR) $$(1)/etc/config
	$(INSTALL_CONF) ./files/zabbix_server.config $$(1)/etc/config/zabbix_server
	$(INSTALL_DIR) $$(1)/etc/uci-defaults
	$(INSTALL_BIN) ./files/zabbix_server.defaults $$(1)/etc/uci-defaults/90_zabbix_server
endef

$(foreach zvariant,tiny openssl gnutls full curl-gnutls,\
  $(eval $(call Package/zabbix-daemon/files,agentd,\
    $(zvariant),\
    ,\
    $(call Package/zabbix-agentd/install-extra))))
$(foreach zvariant,small-postgresql openssl-postgresql gnutls-postgresql full-postgresql curl-gnutls-postgresql openssl-mariadb gnutls-mariadb full-mariadb curl-gnutls-mariadb,\
  $(eval $(call Package/zabbix-daemon/files,server,\
    $(zvariant),\
    $(call Package/zabbix-server/conffiles-extra),\
    $(call Package/zabbix-server/install-extra))))
$(foreach zvariant,tiny small-postgresql openssl-postgresql gnutls-postgresql full-postgresql curl-gnutls-postgresql openssl-mariadb gnutls-mariadb full-mariadb curl-gnutls-mariadb,\
  $(eval $(call Package/zabbix-daemon/files,proxy,\
    $(zvariant))))

# Due to nested defines, eval, and call, the extra spaces for the nested define
# is essential.
define Package/zabbix-server/postinst/Default
        define Package/zabbix-server-$(1)/postinst
  #!/bin/sh
  [ -n "$${IPKG_INSTROOT}" ] || (. /etc/uci-defaults/90_zabbix_server) && rm -f /etc/uci-defaults/90_zabbix_server
  exit 0
         endef
endef

$(foreach zvariant,small-postgresql openssl-postgresql gnutls-postgresql full-postgresql curl-gnutls-postgresql small-mariadb openssl-mariadb gnutls-mariadb curl-gnutls-mariadb,\
  $(eval $(call Package/zabbix-server/postinst/Default,\
    $(zvariant))))

define Package/zabbix-program/files
        define Package/zabbix-$(1)-$(2)/install
		$(call Package/zabbix/install/bin,$$(1),$(1))
        endef
endef

$(foreach zvariant,tiny openssl gnutls,\
  $(eval $(call Package/zabbix-program/files,sender,\
    $(zvariant))))
$(foreach zvariant,tiny openssl gnutls,\
  $(eval $(call Package/zabbix-program/files,get,\
    $(zvariant))))

define Package/zabbix-extra-mac80211/install
	$(call Package/zabbix/install/zabbix.conf.d,$(1),mac80211)
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/zabbix-extra-mac80211/zabbix_helper_mac80211 $(1)/usr/bin/
	chmod 4755 $(1)/usr/bin/zabbix_helper_mac80211
endef

define Package/zabbix-extra-network/install
	$(call Package/zabbix/install/zabbix.conf.d,$(1),network)
	$(INSTALL_DIR) $(1)/usr/share/acl.d
	$(INSTALL_DATA) ./files/zabbix-network-ubus-acl.json $(1)/usr/share/acl.d/zabbix-network.json
endef

define Package/zabbix-extra-network/postinst
#!/bin/sh
if [ -z "$${IPKG_INSTROOT}" ]; then
  killall -s HUP ubusd
fi
endef

define Package/zabbix-extra-wifi/install
	$(call Package/zabbix/install/zabbix.conf.d,$(1),wifi)
	$(INSTALL_DIR) $(1)/usr/share/acl.d
	$(INSTALL_DATA) ./files/zabbix-wifi-ubus-acl.json $(1)/usr/share/acl.d/zabbix-wifi.json
endef

define Package/zabbix-extra-wifi/postinst
#!/bin/sh
if [ -z "$${IPKG_INSTROOT}" ]; then
  killall -s HUP ubusd
fi
endef

define Package/zabbix-frontend-server-postgresql/install
	$(INSTALL_DIR) $(1)/www/zabbix
	$(CP) $(PKG_BUILD_DIR)/ui/* $(1)/www/zabbix
endef

Package/zabbix-frontend-server-mariadb/install = $(Package/zabbix-frontend-server-postgresql/install)
Package/zabbix-frontend-server-extra-auth-postgresql/install = $(Package/zabbix-frontend-server-postgresql/install)
Package/zabbix-frontend-server-extra-auth-mariadb/install = $(Package/zabbix-frontend-server-postgresql/install)

$(eval $(call BuildPackage,zabbix-agentd-tiny))
$(eval $(call BuildPackage,zabbix-agentd-openssl))
$(eval $(call BuildPackage,zabbix-agentd-gnutls))
$(eval $(call BuildPackage,zabbix-agentd-full))
$(eval $(call BuildPackage,zabbix-agentd-curl-gnutls))
$(eval $(call BuildPackage,zabbix-get-tiny))
$(eval $(call BuildPackage,zabbix-get-openssl))
$(eval $(call BuildPackage,zabbix-get-gnutls))
$(eval $(call BuildPackage,zabbix-sender-tiny))
$(eval $(call BuildPackage,zabbix-sender-openssl))
$(eval $(call BuildPackage,zabbix-sender-gnutls))
$(eval $(call BuildPackage,zabbix-proxy-tiny))
$(eval $(call BuildPackage,zabbix-proxy-small-postgresql))
$(eval $(call BuildPackage,zabbix-proxy-openssl-postgresql))
$(eval $(call BuildPackage,zabbix-proxy-gnutls-postgresql))
$(eval $(call BuildPackage,zabbix-proxy-full-postgresql))
$(eval $(call BuildPackage,zabbix-proxy-curl-gnutls-postgresql))
$(eval $(call BuildPackage,zabbix-proxy-small-mariadb))
$(eval $(call BuildPackage,zabbix-proxy-openssl-mariadb))
$(eval $(call BuildPackage,zabbix-proxy-gnutls-mariadb))
$(eval $(call BuildPackage,zabbix-proxy-full-mariadb))
$(eval $(call BuildPackage,zabbix-proxy-curl-gnutls-mariadb))
$(eval $(call BuildPackage,zabbix-server-small-postgresql))
$(eval $(call BuildPackage,zabbix-server-openssl-postgresql))
$(eval $(call BuildPackage,zabbix-server-gnutls-postgresql))
$(eval $(call BuildPackage,zabbix-server-full-postgresql))
$(eval $(call BuildPackage,zabbix-server-curl-gnutls-postgresql))
$(eval $(call BuildPackage,zabbix-server-small-mariadb))
$(eval $(call BuildPackage,zabbix-server-openssl-mariadb))
$(eval $(call BuildPackage,zabbix-server-gnutls-mariadb))
$(eval $(call BuildPackage,zabbix-server-full-mariadb))
$(eval $(call BuildPackage,zabbix-server-curl-gnutls-mariadb))
$(eval $(call BuildPackage,zabbix-extra-mac80211))
$(eval $(call BuildPackage,zabbix-extra-network))
$(eval $(call BuildPackage,zabbix-extra-wifi))
$(eval $(call BuildPackage,zabbix-frontend-server-postgresql))
$(eval $(call BuildPackage,zabbix-frontend-server-mariadb))
$(eval $(call BuildPackage,zabbix-frontend-server-extra-auth-postgresql))
$(eval $(call BuildPackage,zabbix-frontend-server-extra-auth-mariadb))
