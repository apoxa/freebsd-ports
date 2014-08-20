# $FreeBSD$

PORTNAME=	wallabag
PORTVERSION=	1.7.2
CATEGORIES=	www

MAINTAINER=	ben@unpatched.de
COMMENT=	Self hostable application for saving web pages

LICENSE=	WTFPL2
LICENSE_NAME=	Do What The Fuck You Want To Public License version 2
LICENSE_FILE=	${WRKSRC}/COPYING.md
LICENSE_PERMS=	auto-accept dist-mirror dist-sell pkg-mirror pkg-sell

RUN_DEPENDS=	${LOCALBASE}/share/twig/lib/Twig/Autoloader.php:${PORTSDIR}/www/twig-php

USE_PHP=	curl gettext xml
WANT_PHP_WEB=	yes

USE_GITHUB=	yes
GH_ACCOUNT=	wallabag
GH_COMMIT=	af8292c

NO_BUILD=	yes
SUB_FILES=	pkg-message
PLIST_SUB=	WWWOWN=${WWWOWN} \
		WWWGRP=${WWWGRP}

OPTIONS_MULTI=		DB
OPTIONS_MULTI_DB=	MYSQL SQLITE PGSQL
OPTIONS_DEFAULT=	SQLITE
OPTIONS_SUB=		yes

MYSQL_USE=	MYSQL=client PHP=mysql,pdo_mysql
SQLITE_USE=	PHP=pdo_sqlite,sqlite3
PGSQL_USE=	PGSQL=yes PHP=pgsql,pdo_pgsql

do-install:
	@${MKDIR} -m 0755 ${STAGEDIR}${WWWDIR}
	@cd ${WRKSRC} && ${COPYTREE_SHARE} . ${STAGEDIR}${WWWDIR}

.include <bsd.port.mk>
