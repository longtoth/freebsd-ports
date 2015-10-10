# Created by: Nick Chevsky <nchevsky@blazis.com>
# $FreeBSD$

PORTNAME=	mfi
PORTVERSION=	2.1.11
CATEGORIES=	net-mgmt java
MASTER_SITES=	http://dl.ubnt.com/mfi/${PORTVERSION}/
DISTNAME=	mFi.unix

MAINTAINER=	nchevsky@blazis.com
COMMENT=	Ubiquiti mFi Controller

RUN_DEPENDS=	mongodb<=2.4.10:${PORTSDIR}/databases/mongodb

RESTRICTED=	The distfile includes a firmware image that may only be downloaded from the official mirror.

USES=		zip
USE_JAVA=	yes
USE_RC_SUBR=	${PORTNAME}
JAVA_VERSION=	1.6+
JAVA_OS=	native
JAVA_RUN=	yes
NO_ARCH=	yes
NO_BUILD=	yes

DATADIR=	${JAVASHAREDIR}/${PORTNAME}
DBDIR=		/var/db/${PORTNAME}
LOGDIR=		/var/log/${PORTNAME}
TMPDIR=		/tmp/${PORTNAME}
WRKSRC=		${WRKDIR}/mFi

PLIST_SUB+=	DBDIR=${DBDIR} ETCDIR=${ETCDIR} LOGDIR=${LOGDIR} TMPDIR=${TMPDIR}
SUB_FILES+=	pkg-deinstall pkg-message
SUB_LIST+=	DBDIR=${DBDIR} ETCDIR=${ETCDIR} HOSTNAME=`hostname` LOGDIR=${LOGDIR} PORTNAME=${PORTNAME} TMPDIR=${TMPDIR}

post-extract:
	# extract web application archive
	@${MKDIR} ${WRKSRC}/webapps/ROOT/ && \
	${TAR} -xf ${WRKSRC}/webapps/ROOT.war -C ${WRKSRC}/webapps/ROOT/ && \
	${RM} ${WRKSRC}/webapps/ROOT.war

do-install:
	# copy files
	@cd ${WRKSRC} && ${COPYTREE_SHARE} . ${STAGEDIR}${DATADIR}

post-install:
	# create directories
	@${MKDIR} ${STAGEDIR}${DBDIR}
	@${MKDIR} ${STAGEDIR}${DBDIR}/backup
	@${MKDIR} ${STAGEDIR}${ETCDIR}
	@${MKDIR} ${STAGEDIR}${ETCDIR}/Catalina
	@${MKDIR} ${STAGEDIR}${ETCDIR}/Catalina/localhost
	@${MKDIR} ${STAGEDIR}${LOGDIR}
	@${MKDIR} ${STAGEDIR}${TMPDIR}
	# move things that will be symlinked
	@${MV} ${STAGEDIR}${DATADIR}/conf/* ${STAGEDIR}${ETCDIR} && ${RMDIR} ${STAGEDIR}${DATADIR}/conf
	@${MV} ${STAGEDIR}${DATADIR}/data/* ${STAGEDIR}${DBDIR} && ${RMDIR} ${STAGEDIR}${DATADIR}/data
	@${MV} ${STAGEDIR}${DBDIR}/system.properties ${STAGEDIR}${ETCDIR}/${PORTNAME}.conf.sample
	# create symlinks
	@${LN} -s ${DBDIR}  ${STAGEDIR}${DATADIR}/data
	@${LN} -s ${ETCDIR} ${STAGEDIR}${DATADIR}/conf
	@${LN} -s ${ETCDIR}/${PORTNAME}.conf ${STAGEDIR}${DBDIR}/system.properties
	@${LN} -s ${LOCALBASE}/bin/mongod ${STAGEDIR}${DATADIR}/bin/mongod
	@${LN} -s ${LOGDIR} ${STAGEDIR}${DATADIR}/logs
	@${LN} -s ${TMPDIR} ${STAGEDIR}${DATADIR}/work

.include <bsd.port.mk>
