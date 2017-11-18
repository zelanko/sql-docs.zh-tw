---
title: "SQLServerConnectionPoolDataSource 成員 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: dac0337e-8088-488c-a25a-801a2190f6ca
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: da18ece75049aa2681379f265e9812159017d722
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlserverconnectionpooldatasource-members"></a>SQLServerConnectionPoolDataSource 成員
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  下表列出所公開的成員[SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)類別。  
  
## <a name="constructors"></a>建構函式  
  
|名稱|Description|  
|----------|-----------------|  
|[SQLServerConnectionPoolDataSource （)](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-constructor.md)|初始化的新執行個體[SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)類別。|  
  
## <a name="fields"></a>欄位  
 無。  
  
## <a name="inherited-fields"></a>繼承的欄位  
 無。  
  
## <a name="methods"></a>方法  
  
|名稱|Description|  
|----------|-----------------|  
|[getApplicationIntent](../../../connect/jdbc/reference/getapplicationintent-method-sqlserverdatasource.md)|(繼承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 傳回的值**applicationIntent**連接屬性。|  
|[getApplicationName](../../../connect/jdbc/reference/getapplicationname-method-sqlserverdatasource.md)|(繼承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 傳回應用程式名稱。|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md)|(繼承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 嘗試建立與這個資料來源物件所代表的資料來源的連接。|  
|[getDatabaseName](../../../connect/jdbc/reference/getdatabasename-method-sqlserverdatasource.md)|(繼承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 傳回的資料庫名稱。|  
|[getDescription](../../../connect/jdbc/reference/getdescription-method-sqlserverdatasource.md)|(繼承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 傳回的資料來源的描述。|  
|[getFailoverPartner](../../../connect/jdbc/reference/getfailoverpartner-method-sqlserverdatasource.md)|(繼承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 傳回資料庫鏡像組態中使用的容錯移轉伺服器名稱。|  
|[getInstanceName](../../../connect/jdbc/reference/getinstancename-method-sqlserverdatasource.md)|(繼承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 傳回[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]執行個體名稱。|  
|[getLastUpdateCount](../../../connect/jdbc/reference/getlastupdatecount-method-sqlserverdatasource.md)|(繼承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 傳回**布林**值，指出是否啟用 lastUpdateCount 屬性。|  
|[getLockTimeout](../../../connect/jdbc/reference/getlocktimeout-method-sqlserverdatasource.md)|(繼承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 傳回**int**值，指出資料庫要等候報告鎖定逾時之前的毫秒數。|  
|[getLoginTimeout](../../../connect/jdbc/reference/getlogintimeout-method-sqlserverdatasource.md)|(繼承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 會傳回此資料來源物件會嘗試建立連接時等待的秒數。|  
|[getLogWriter](../../../connect/jdbc/reference/getlogwriter-method-sqlserverdatasource.md)|(繼承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 會傳回要用於所有記錄和追蹤訊息的字元輸出資料流。|  
|[getMultiSubnetFailover](../../../connect/jdbc/reference/getmultisubnetfailover-method-sqlserverdatasource.md)|(繼承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 傳回的值**multiSubnetFailover**連接屬性。|  
|[getPooledConnection](../../../connect/jdbc/reference/getpooledconnection-method-sqlserverconnectionpooldatasource.md)|嘗試建立可用來當做共用連接的實體資料庫連接。|  
|[getPortNumber](../../../connect/jdbc/reference/getportnumber-method-sqlserverdatasource.md)|(繼承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 會傳回目前用來與通訊的連接埠號碼[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。|  
|[getReference](../../../connect/jdbc/reference/getreference-method-sqlserverconnectionpooldatasource.md)|傳回此資料來源物件的參考。|  
|[getSelectMethod](../../../connect/jdbc/reference/getselectmethod-method-sqlserverdatasource.md)|(繼承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 傳回用於建立使用這個資料來源物件的所有結果集的預設資料指標類型。|  
|[getSendStringParametersAsUnicode](../../../connect/jdbc/reference/getsendstringparametersasunicode-method-sqlserverdatasource.md)|(繼承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 傳回**布林**值，指出是否啟用伺服器以 UNICODE 格式傳送字串參數。|  
|[getServerName](../../../connect/jdbc/reference/getservername-method-sqlserverdatasource.md)|(繼承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 傳回正在執行的電腦名稱[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。|  
|[getURL](../../../connect/jdbc/reference/geturl-method-sqlserverdatasource.md)|(繼承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 傳回用來連接到資料來源的 URL。|  
|[getUser](../../../connect/jdbc/reference/getuser-method-sqlserverdatasource.md)|(繼承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 傳回用來連接資料來源的使用者名稱。|  
|[getWorkstationID](../../../connect/jdbc/reference/getworkstationid-method-sqlserverdatasource.md)|(繼承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 傳回用戶端的名稱用來連接到資料來源的電腦名稱。|  
|[getXopenStates](../../../connect/jdbc/reference/getxopenstates-method-sqlserverdatasource.md)|(繼承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 傳回**布林**值，指出是否啟用將 SQL 狀態轉換成 XOPEN 標準狀態。|  
|[isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverconnectionpooldatasource.md)|指出這個物件是否為指定之介面的包裝函式。|  
|[setApplicationIntent](../../../connect/jdbc/reference/setapplicationintent-method-sqlserverdatasource.md)|(繼承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 設定的值**applicationIntent**連接屬性。|  
|[setApplicationName](../../../connect/jdbc/reference/setapplicationname-method-sqlserverdatasource.md)|(繼承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 設定應用程式名稱。|  
|[setAuthenticationSceme](../../../connect/jdbc/reference/setauthenticationscheme-sqlserverdatasource.md)|(繼承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 表示您想要使用的應用程式的整合式安全性種類。|  
|[setDatabaseName](../../../connect/jdbc/reference/setdatabasename-method-sqlserverdatasource.md)|(繼承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 設定要連接到的資料庫名稱。|  
|[setDescription](../../../connect/jdbc/reference/setdescription-method-sqlserverdatasource.md)|(繼承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 設定資料來源的描述。|  
|[setFailoverPartner](../../../connect/jdbc/reference/setfailoverpartner-method-sqlserverdatasource.md)|(繼承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 設定資料庫鏡像組態中所使用的容錯移轉伺服器名稱。|  
|[setInstanceName](../../../connect/jdbc/reference/setinstancename-method-sqlserverdatasource.md)|(繼承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 集[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]執行個體名稱。|  
|[setIntegratedSecurity](../../../connect/jdbc/reference/setintegratedsecurity-method-sqlserverdatasource.md)|(繼承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 集**布林**值，指出是否啟用 integratedSecurity 屬性。|  
|[setLastUpdateCount](../../../connect/jdbc/reference/setlastupdatecount-method-sqlserverdatasource.md)|(繼承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 集**布林**值，指出是否啟用 lastUpdateCount 屬性。|  
|[setLockTimeout](../../../connect/jdbc/reference/setlocktimeout-method-sqlserverdatasource.md)|(繼承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 集**int**值，指出資料庫報告鎖定逾時之前要等候的毫秒數。|  
|[setLoginTimeout](../../../connect/jdbc/reference/setlogintimeout-method-sqlserverdatasource.md)|(繼承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 設定此資料來源物件會嘗試建立連接時等待的秒數。|  
|[setLogWriter](../../../connect/jdbc/reference/setlogwriter-method-sqlserverdatasource.md)|(繼承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 設定要用於所有記錄和追蹤訊息的字元輸出資料流。|  
|[setMultiSubnetFailover](../../../connect/jdbc/reference/setmultisubnetfailover-method-sqlserverdatasource.md)|(繼承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 設定的值**multiSubnetFailover**連接屬性。|  
|[setPassword](../../../connect/jdbc/reference/setpassword-method-sqlserverdatasource.md)|(繼承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 設定將用來連接到的密碼[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。|  
|[setPortNumber](../../../connect/jdbc/reference/setportnumber-method-sqlserverdatasource.md)|(繼承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 設定用來與通訊的連接埠號碼[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。|  
|[setSelectMethod](../../../connect/jdbc/reference/setselectmethod-method-sqlserverdatasource.md)|(繼承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 設定用於建立使用這個資料來源物件的所有結果集的預設資料指標類型。|  
|[setSendStringParametersAsUnicode](../../../connect/jdbc/reference/setsendstringparametersasunicode-method-sqlserverdatasource.md)|(繼承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 集**布林**值，指出是否啟用伺服器以 UNICODE 格式傳送字串參數。|  
|[setServerName](../../../connect/jdbc/reference/setservername-method-sqlserverdatasource.md)|(繼承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 設定正在執行的電腦名稱[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。|  
|[setURL](../../../connect/jdbc/reference/seturl-method-sqlserverdatasource.md)|(繼承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 設定用來連接到資料來源的 URL。|  
|[setUser](../../../connect/jdbc/reference/setuser-method-sqlserverdatasource.md)|(繼承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 設定用來連接資料來源的使用者名稱。|  
|[setWorkstationID](../../../connect/jdbc/reference/setworkstationid-method-sqlserverdatasource.md)|(繼承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 設定用戶端用來連接到資料來源的電腦名稱。|  
|[setXopenStates](../../../connect/jdbc/reference/setxopenstates-method-sqlserverdatasource.md)|(繼承自[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 集**布林**值，指出是否啟用將 SQL 狀態轉換成 XOPEN 標準狀態。|  
|[解除包裝](../../../connect/jdbc/reference/unwrap-method-sqlserverconnectionpooldatasource.md)|傳回物件，用於實作指定的介面，以允許存取[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]-特有的方法。|  
  
## <a name="inherited-methods"></a>繼承的方法  
  
|類別繼承自：|方法|  
|---------------------------|-------------|  
|com.microsoft.sqlserver.jdbc.SQLServerDataSource|getApplicationName, getConnection, getDatabaseName, getDescription, getFailoverPartner, getInstanceName, getLastUpdateCount, getLockTimeout, getLoginTimeout, getLogWriter, getPortNumber, getSelectMethod, getSendStringParametersAsUnicode, getServerName, getURL, getUser, getWorkstationID, getXopenStates, setApplicationName, setDatabaseName, setDescription, setFailoverPartner, setInstanceName, setIntegratedSecurity, setLastUpdateCount, setLockTimeout, setLoginTimeout, setLogWriter, setPassword, setPortNumber, setSelectMethod, setSendStringParametersAsUnicode, setServerName, setURL, setUser, setWorkstationID, setXopenStates|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Wrapper|isWrapperFor, unwrap|  
|javax.sql.ConnectionPoolDataSource|getLoginTimeout, getLogWriter, setLoginTimeout, setLogWriter, getPooledConnection|  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerConnectionPoolDataSource 類別](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)  
  
  

