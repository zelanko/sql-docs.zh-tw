---
title: SQLServerDataSource 成員 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7e749bc5-d765-4864-be2b-7822d4c20c09
caps.latest.revision: 43
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 895de703b966fe4b99a03add2634f40c39c02449
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sqlserverdatasource-members"></a>SQLServerDataSource 成員
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  下表列出所公開的成員[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)類別。  
  
## <a name="constructors"></a>建構函式  
  
|名稱|Description|  
|----------|-----------------|  
|[（SQLServerDataSource)](../../../connect/jdbc/reference/sqlserverdatasource-constructor.md)|初始化的新執行個體[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)類別。|  
  
## <a name="fields"></a>欄位  
 無。  
  
## <a name="inherited-fields"></a>繼承的欄位  
 無。  
  
## <a name="methods"></a>方法  
  
|名稱|Description|  
|----------|-----------------|  
|[getApplicationIntent](../../../connect/jdbc/reference/getapplicationintent-method-sqlserverdatasource.md)|傳回的值**applicationIntent**連接屬性。|  
|[getApplicationName](../../../connect/jdbc/reference/getapplicationname-method-sqlserverdatasource.md)|傳回應用程式名稱。|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md)|嘗試建立連接的資料來源這個[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)物件表示。|  
|[getDatabaseName](../../../connect/jdbc/reference/getdatabasename-method-sqlserverdatasource.md)|傳回資料庫名稱。|  
|[getDisableStatementPooling](../../../connect/jdbc/reference/getdisablestatementpooling-method-sqlserverdatasource.md)|傳回的值**disableStatementPooling**連接屬性。 此設定會控制是否會啟用共用陳述式或不適用於此連線。|  
|[getEnablePrepareOnFirstPreparedStatementCall](../../../connect/jdbc/reference/getenableprepareonfirstpreparedstatementcall-method-sqlserverdatasource.md)|傳回的值**enablePrepareOnFirstPreparedStatementCall**連接屬性。|  
|[getEncrypt](../../../connect/jdbc/reference/getencrypt-method-sqlserverdatasource.md)|傳回**布林**值，指出是否啟用 encrypt 屬性。|  
|[getDescription](../../../connect/jdbc/reference/getdescription-method-sqlserverdatasource.md)|傳回資料來源的描述。|  
|[getFailoverPartner](../../../connect/jdbc/reference/getfailoverpartner-method-sqlserverdatasource.md)|傳回用於資料庫鏡像組態的容錯移轉伺服器名稱。|  
|[getHostNameInCertificate](../../../connect/jdbc/reference/gethostnameincertificate-method-sqlserverdatasource.md)|傳回用於驗證 SQL Server 安全通訊端層 (SSL) 憑證的主機名稱。|  
|[getInstanceName](../../../connect/jdbc/reference/getinstancename-method-sqlserverdatasource.md)|傳回[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]執行個體名稱。|  
|[getLastUpdateCount](../../../connect/jdbc/reference/getlastupdatecount-method-sqlserverdatasource.md)|傳回**布林**值，指出是否啟用 lastUpdateCount 屬性。|  
|[getLockTimeout](../../../connect/jdbc/reference/getlocktimeout-method-sqlserverdatasource.md)|傳回**int**值，指出資料庫在報告鎖定逾時之前要等候的毫秒數。|  
|[getLoginTimeout](../../../connect/jdbc/reference/getlogintimeout-method-sqlserverdatasource.md)|傳回此秒數[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)物件在嘗試建立連接時的等候。|  
|[getLogWriter](../../../connect/jdbc/reference/getlogwriter-method-sqlserverdatasource.md)|傳回要用於所有記錄和追蹤訊息的字元輸出資料流。|  
|[getMultiSubnetFailover](../../../connect/jdbc/reference/getmultisubnetfailover-method-sqlserverdatasource.md)|傳回的值**multiSubnetFailover**連接屬性。|  
|[getPacketSize](../../../connect/jdbc/reference/getpacketsize-method-sqlserverdatasource.md)|傳回用來與通訊的目前網路封包大小[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]，以位元組為單位指定。|  
|[getPortNumber](../../../connect/jdbc/reference/getportnumber-method-sqlserverdatasource.md)|傳回目前用來與通訊埠編號[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。|  
|[getReference](../../../connect/jdbc/reference/getreference-method-sqlserverdatasource.md)|將參考傳回給這[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)物件。|  
|[getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverdatasource.md)|傳回的回應緩衝模式，這個[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)物件。|  
|[getSelectMethod](../../../connect/jdbc/reference/getselectmethod-method-sqlserverdatasource.md)|傳回用於建立使用這項功能的所有結果集的預設資料指標類型[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)物件。|  
|[getSendStringParametersAsUnicode](../../../connect/jdbc/reference/getsendstringparametersasunicode-method-sqlserverdatasource.md)|傳回**布林**值，指出是否啟用伺服器以 UNICODE 格式傳送字串參數。|  
|[getSendTimeAsDatetime](../../../connect/jdbc/reference/getsendtimeasdatetime-method-sqlserverdatasource.md)|傳回設定**SendTimeAsDatetime**連接屬性。|  
|[getServerName](../../../connect/jdbc/reference/getservername-method-sqlserverdatasource.md)|傳回執行之電腦的名稱[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。|  
|[getServerPreparedStatementDiscardThreshold](../../../connect/jdbc/reference/getserverpreparedstatementdiscardthreshold-method-sqlserverdatasource.md)|傳回的值**serverPreparedStatementDiscardThreshold**連接屬性。|  
|[getStatementPoolingCacheSize](../../../connect/jdbc/reference/getstatementpoolingcachesize-method-sqlserverdatasource.md)|傳回此連線的已備妥的陳述式快取大小。|  
|[getTrustManagerClass](../../../connect/jdbc/reference/gettrustmanagerclass-method-sqlserverdatasource.md)|傳回 TrustManagerClass 連接屬性的字串值。|  
|[getTrustManagerConstructorArg](../../../connect/jdbc/reference/gettrustmanagerconstructorarg-method-sqlserverdatasource.md)|傳回 TrustManagerConstructorArg 連接屬性的字串值。|  
|[getTrustServerCertificate](../../../connect/jdbc/reference/gettrustservercertificate-method-sqlserverdatasource.md)|傳回**布林**值，指出是否啟用 trustServerCertificate 屬性。|  
|[getTrustStore](../../../connect/jdbc/reference/gettruststore-method-sqlserverdatasource.md)|傳回憑證 trustStore 檔案的路徑 (包括檔案名稱)。|  
|[getURL](../../../connect/jdbc/reference/geturl-method-sqlserverdatasource.md)|傳回用來連接到資料來源的 URL。|  
|[getUser](../../../connect/jdbc/reference/getuser-method-sqlserverdatasource.md)|傳回用來連接到資料來源的使用者名稱。|  
|[getUseSQLServerBaseDate](../../../connect/jdbc/reference/getsendtimeasdatetime-method-sqlserverdatasource.md)|傳回 useSQLServerBaseDate 連接屬性的設定。|  
|[getWorkstationID](../../../connect/jdbc/reference/getworkstationid-method-sqlserverdatasource.md)|傳回用來連接到資料來源之用戶端電腦的名稱。|  
|[getXopenStates](../../../connect/jdbc/reference/getxopenstates-method-sqlserverdatasource.md)|傳回**布林**值，指出是否啟用將 SQL 狀態轉換成 XOPEN 標準狀態。|  
|[isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverdatasource.md)|指出這個資料來源物件是否為指定之介面的包裝函式。|  
|[setApplicationIntent](../../../connect/jdbc/reference/setapplicationintent-method-sqlserverdatasource.md)|設定的值**applicationIntent**連接屬性。|  
|[setApplicationName](../../../connect/jdbc/reference/setapplicationname-method-sqlserverdatasource.md)|設定應用程式名稱。|  
|[setAuthenticationScheme](../../../connect/jdbc/reference/setauthenticationscheme-sqlserverdatasource.md)|表示您希望應用程式使用的整合式安全性種類。|  
|[setDatabaseName](../../../connect/jdbc/reference/setdatabasename-method-sqlserverdatasource.md)|設定要連接的資料庫名稱。|  
|[setDescription](../../../connect/jdbc/reference/setdescription-method-sqlserverdatasource.md)|設定資料來源的描述。|  
|[setDisableStatementPooling](../../../connect/jdbc/reference/setdisablestatementpooling-method-sqlserverdatasource.md)|設定為 true 或 false 的陳述式集區。|  
|[setEnablePrepareOnFirstPreparedStatementCall](../../../connect/jdbc/reference/setenableprepareonfirstpreparedstatementcall-method-sqlserverdatasource.md)|指定的新值**enablePrepareOnFirstPreparedStatementCall**連接屬性。|  
|[setEncrypt](../../../connect/jdbc/reference/setencrypt-method-sqlserverdatasource.md)|設定**布林**值，指出是否啟用 encrypt 屬性。|  
|[setFailoverPartner](../../../connect/jdbc/reference/setfailoverpartner-method-sqlserverdatasource.md)|設定用於資料庫鏡像組態的容錯移轉伺服器名稱。|  
|[setHostNameInCertificate](../../../connect/jdbc/reference/sethostnameincertificate-method-sqlserverdatasource.md)|設定用於驗證 SQL Server 安全通訊端層 (SSL) 憑證的主機名稱。|  
|[setInstanceName](../../../connect/jdbc/reference/setinstancename-method-sqlserverdatasource.md)|設定[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]執行個體名稱。|  
|[setIntegratedSecurity](../../../connect/jdbc/reference/setintegratedsecurity-method-sqlserverdatasource.md)|設定**布林**值，指出是否啟用 integratedSecurity 屬性。|  
|[setLastUpdateCount](../../../connect/jdbc/reference/setlastupdatecount-method-sqlserverdatasource.md)|設定**布林**值，指出是否啟用 lastUpdateCount 屬性。|  
|[setLockTimeout](../../../connect/jdbc/reference/setlocktimeout-method-sqlserverdatasource.md)|設定**int**值，表示要等候資料庫報告鎖定逾時之前的毫秒數。|  
|[setLoginTimeout](../../../connect/jdbc/reference/setlogintimeout-method-sqlserverdatasource.md)|設定的秒數，這[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)物件在嘗試建立連接時的等候。|  
|[setLogWriter](../../../connect/jdbc/reference/setlogwriter-method-sqlserverdatasource.md)|設定要用於所有記錄和追蹤訊息的字元輸出資料流。|  
|[setMultiSubnetFailover](../../../connect/jdbc/reference/setmultisubnetfailover-method-sqlserverdatasource.md)|設定的值**multiSubnetFailover**連接屬性。|  
|[setPacketSize](../../../connect/jdbc/reference/setpacketsize-method-sqlserverdatasource.md)|設定用來與通訊的目前網路封包大小[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]，以位元組為單位指定。|  
|[setPassword](../../../connect/jdbc/reference/setpassword-method-sqlserverdatasource.md)|設定用來連接到的密碼[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。|  
|[setPortNumber](../../../connect/jdbc/reference/setportnumber-method-sqlserverdatasource.md)|設定用來與通訊埠編號[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。|  
|[setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverdatasource.md)|設定的回應緩衝模式為使用這項功能所建立的連線[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)物件。|  
|[setSelectMethod](../../../connect/jdbc/reference/setselectmethod-method-sqlserverdatasource.md)|設定用於建立使用這項功能的所有結果集的預設資料指標類型[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)物件。|  
|[setSendStringParametersAsUnicode](../../../connect/jdbc/reference/setsendstringparametersasunicode-method-sqlserverdatasource.md)|設定**布林**值，指出是否啟用伺服器以 UNICODE 格式傳送字串參數。|  
|[setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md)|指定如何將 java.sql.Time 值傳送給伺服器。|  
|[setServerName](../../../connect/jdbc/reference/setservername-method-sqlserverdatasource.md)|設定執行的電腦名稱[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。|  
|[setServerPreparedStatementDiscardThreshold](../../../connect/jdbc/reference/setserverpreparedstatementdiscardthreshold-method-sqlserverdatasource.md)|設定的新值**serverPreparedStatementDiscardThreshold**連接屬性。|  
|[setStatementPoolingCacheSize](../../../connect/jdbc/reference/setstatementpoolingcachesize-method-sqlserverdatasource.md)|設定此連線的已備妥的陳述式快取的大小。|  
|[setTrustManagerClass](../../../connect/jdbc/reference/settrustmanagerclass-method-sqlserverdatasource.md)|設定 TrustManagerClass 連接屬性的字串值。|  
|[setTrustManagerConstructorArg](../../../connect/jdbc/reference/settrustmanagerconstructorarg-method-sqlserverdatasource.md)|設定 TrustManagerConstructorArg 連接屬性的字串值。|  
|[setTrustServerCertificate](../../../connect/jdbc/reference/settrustservercertificate-method-sqlserverdatasource.md)|設定**布林**值，指出是否啟用 trustServerCertificate 屬性。|  
|[setTrustStore](../../../connect/jdbc/reference/settruststore-method-sqlserverdatasource.md)|設定憑證 trustStore 檔案的路徑 (包括檔案名稱)。|  
|[setTrustStorePassword](../../../connect/jdbc/reference/settruststorepassword-method-sqlserverdatasource.md)|設定用來檢查 trustStore 資料完整性的密碼。|  
|[setURL](../../../connect/jdbc/reference/seturl-method-sqlserverdatasource.md)|設定用來連接到資料來源的 URL。|  
|[setUser](../../../connect/jdbc/reference/setuser-method-sqlserverdatasource.md)|設定用來連接到資料來源的使用者名稱。|  
|[setWorkstationID](../../../connect/jdbc/reference/setworkstationid-method-sqlserverdatasource.md)|設定用來連接到資料來源之用戶端電腦的名稱。|  
|[setXopenStates](../../../connect/jdbc/reference/setxopenstates-method-sqlserverdatasource.md)|設定**布林**值，指出是否啟用將 SQL 狀態轉換成 XOPEN 標準狀態。|  
|[解除包裝](../../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md)|傳回物件，用於實作指定的介面，以允許存取[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]-特有的方法。|  
  
## <a name="inherited-methods"></a>繼承的方法  
  
|類別繼承自：|方法|  
|---------------------------|-------------|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Wrapper|isWrapperFor, unwrap|  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
