# $FreeBSD$

PORTNAME=		zlib
PORTVERSION=	20140818
CATEGORIES=		archivers
PKGNAMEPREFIX=  ${LUA_PKGNAMEPREFIX}

MAINTAINER=		ben@unpatched.de
COMMENT=		Simple streaming interface to zlib for Lua

LICENSE=		MIT

USE_GITHUB=		yes
GH_ACCOUNT=		brimworks
GH_PROJECT=		lua-zlib
GH_COMMIT=		c0014bc
GH_TAGNAME=		${GH_COMMIT}

USES=			pkgconfig lua:51 cmake

PLIST_FILES=	%%LUA_MODLIBDIR%%/zlib.so

do-install:
	${MKDIR} ${STAGEDIR}${LUA_MODLIBDIR}
	${INSTALL_PROGRAM} ${WRKSRC}/zlib.so ${STAGEDIR}${LUA_MODLIBDIR}

.include <bsd.port.mk>
