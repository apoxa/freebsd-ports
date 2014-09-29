# $FreeBSD$

PORTNAME=	weechat
PORTVERSION=	1.0.1
CATEGORIES=	irc
MASTER_SITES=	http://weechat.org/files/src/

MAINTAINER=	jase@FreeBSD.org
COMMENT=	Lightweight and user friendly ncurses based IRC client

LICENSE=	GPLv3

LIB_DEPENDS=	libcurl.so:${PORTSDIR}/ftp/curl \
		libgcrypt.so:${PORTSDIR}/security/libgcrypt

CONFLICTS=	weechat-devel-1.*

USE_LDCONFIG=	yes
USES=		cmake iconv ncurses
CMAKE_ARGS+=	-DENABLE_GUILE=no
CFLAGS+=	-I${LOCALBASE}/include -L${LOCALBASE}/lib

OPTIONS_DEFINE=	RUBY PYTHON PERL TCL LUA CHARSET BACKTRACE ASPELL \
		GNUTLS NLS ICON CA_BUNDLE MANPAGES DOCS
OPTIONS_DEFAULT=RUBY PYTHON PERL TCL LUA CHARSET BACKTRACE ASPELL \
		GNUTLS CA_BUNDLE ICON MANPAGES
OPTIONS_SUB=	yes

BACKTRACE_DESC=	Provide crash backtraces
CHARSET_DESC=	Charset conversion support
ICON_DESC=		Desktop icon
CA_BUNDLE_DESC=	Use CA bundle from Mozilla Project

CA_BUNDLE_RUN_DEPENDS=	${LOCALBASE}/share/certs/ca-root-nss.crt:${PORTSDIR}/security/ca_root_nss
CA_BUNDLE_CMAKE_ON=		-DCA_FILE=${LOCALBASE}/share/certs/ca-root-nss.crt

CHARSET_CMAKE_OFF=	-DENABLE_CHARSET=no

NLS_USES=		gettext
NLS_CMAKE_OFF=	-DENABLE_NLS=no

ASPELL_LIB_DEPENDS=	libaspell.so:${PORTSDIR}/textproc/aspell
ASPELL_CMAKE_OFF=	-DENABLE_ASPELL=no

PYTHON_USES=	python:2
PYTHON_CMAKE_OFF=	-DENABLE_PYTHON=no

GNUTLS_USES=			pkgconfig
GNUTLS_LIB_DEPENDS=		libgnutls.so:${PORTSDIR}/security/gnutls
GNUTLS_CMAKE_OFF=		-DENABLE_GNUTLS=no

PERL_USES=				perl5
PERL_CMAKE_ARGS_OFF=	-DENABLE_PERL=no

TCL_USES=	tcl:85+
TCL_CMAKE_OFF=	-DENABLE_TCL=no

LUA_USES=	lua:51
LUA_CMAKE_OFF=	-DENABLE_LUA=no

BACKTRACE_LIB_DEPENDS=	libexecinfo.so:${PORTSDIR}/devel/libexecinfo

MANPAGES_BUILD_DEPENDS=	xsltproc:${PORTSDIR}/textproc/libxslt \
		docbook-xsl>=0:${PORTSDIR}/textproc/docbook-xsl \
		docbook-xml>=0:${PORTSDIR}/textproc/docbook-xml \
		asciidoc:${PORTSDIR}/textproc/asciidoc
MANPAGES_CMAKE_ON=	-DENABLE_MAN=yes -DMANDIR=${MANPREFIX}/man
MANPAGES_CMAKE_OFF=	-DENABLE_MAN=no

DOCS_BUILD_DEPENDS=	asciidoc:${PORTSDIR}/textproc/asciidoc \
		source-highlight>=3.1.5:${PORTSDIR}/textproc/source-highlight
DOCS_CMAKE_ON=	-DENABLE_DOC=yes
DOCS_CMAKE_OFF=	-DENABLE_DOC=no

RUBY_USE=	RUBY=yes
RUBY_CMAKE_OFF=	-DENABLE_RUBY=no

.include <bsd.port.options.mk>

post-patch:
	@${REINPLACE_CMD} -e 's|$${LIBDIR}/../pkgconfig|$${CMAKE_INSTALL_PREFIX}/libdata/pkgconfig|' ${WRKSRC}/CMakeLists.txt
.for f in src/CMakeLists.txt src/core/CMakeLists.txt cmake/*.cmake
	@${REINPLACE_CMD} -e 's|/usr/local|${LOCALBASE}|' ${WRKSRC}/${f}
.endfor
.if ! ${PORT_OPTIONS:MBACKTRACE}
	@${REINPLACE_CMD} -e '/if.*FreeBSD/,/endif/d' ${WRKSRC}/src/core/CMakeLists.txt
.endif
.if ! ${PORT_OPTIONS:MICON}
	@${REINPLACE_CMD} -e '/^# icon$$/,/^$$/d' ${WRKSRC}/CMakeLists.txt
.endif

.include <bsd.port.mk>
