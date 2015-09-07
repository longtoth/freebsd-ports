# Created by: Nick Chevsky <nchevsky@blazis.com>
# $FreeBSD$

PORTNAME=	hdhomerun
PORTVERSION=	20150901
DISTVERSIONSUFFIX=	atest1
CATEGORIES=	multimedia
MASTER_SITES=	http://download.silicondust.com/hdhomerun/
PKGNAMESUFFIX=	-record
DISTNAME=	${PORTNAME}_record_freebsd_${PORTVERSION}${DISTVERSIONSUFFIX}
EXTRACT_SUFX=

MAINTAINER=	nchevsky@blazis.com
COMMENT=	HDHomeRun DVR recording engine by SiliconDust

RESTRICTED=	SiliconDust has not authorized redistribution of the binaries.

NO_BUILD=	yes
ONLY_FOR_ARCHS=	amd64
USE_RC_SUBR=	${PORTNAME}

BINDIR=		${PREFIX}/sbin
BINNAME=	${PORTNAME}${PKGNAMESUFFIX}
ETCDIR=		${PREFIX}/etc

PLIST_SUB+=	BINDIR=${BINDIR} BINNAME=${BINNAME} ETCDIR=${ETCDIR} PORTNAME=${PORTNAME}
SUB_FILES+=	pkg-deinstall pkg-message
SUB_LIST+=	BINDIR=${BINDIR} BINNAME=${BINNAME} ETCDIR=${ETCDIR} PORTNAME=${PORTNAME}

do-extract:
	@${MKDIR} ${WRKSRC}
	@${CP} ${DISTDIR}/${DISTFILES} ${WRKSRC}/${BINNAME}
	@${CHMOD} a+x ${WRKSRC}/${BINNAME}

do-install:
	${INSTALL_PROGRAM} ${WRKSRC}/${BINNAME} ${STAGEDIR}/${BINDIR}
	${INSTALL_DATA} ${FILESDIR}/*.conf.sample ${STAGEDIR}/${ETCDIR}

.include <bsd.port.mk>
