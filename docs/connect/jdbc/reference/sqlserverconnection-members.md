---
description: SQLServerConnection 成員
title: SQLServerConnection 成員 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3115a533-756b-4c78-aee9-4ba7253c85e0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 75a3670a0f7e958f1976e387acdaa02a8449d202
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88458280"
---
# <a name="sqlserverconnection-members"></a>SQLServerConnection 成員
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  下表列出由 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 類別公開的成員。  
  
## <a name="constructors"></a>建構函式  
 無。  
  
## <a name="fields"></a>欄位  
  
|名稱|描述|  
|----------|-----------------|  
|[TRANSACTION_SNAPSHOT](../../../connect/jdbc/reference/transaction-snapshot-field-sqlserverconnection.md)|用來指定快照集交易隔離等級。|  
  
## <a name="inherited-fields"></a>繼承的欄位  
  
|類別繼承自：|描述|  
|---------------------------|-----------------|  
|java.sql.Connection|TRANSACTION_NONE, TRANSACTION_READ_COMMITTED, TRANSACTION_READ_UNCOMMITTED, TRANSACTION_REPEATABLE_READ, TRANSACTION_SERIALIZABLE|  
  
## <a name="methods"></a>方法  
  
|名稱|描述|  
|----------|-----------------|  
|[clearWarnings](../../../connect/jdbc/reference/clearwarnings-method-sqlserverconnection.md)|清除這個 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 物件所報告的所有警告。|  
|[close](../../../connect/jdbc/reference/close-method-sqlserverconnection.md)|立刻釋放出這個 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 物件的資料庫和 JDBC 資源，而非等待它們由系統自動釋放。|  
|[closeUnreferencedPreparedStatementHandles](../../../connect/jdbc/reference/closeunreferencedpreparedstatementhandles-method-sqlserverconnection.md)|強制執行任何未完成捨棄備妥陳述式的未準備要求。| 
|[commit](../../../connect/jdbc/reference/commit-method-sqlserverconnection.md)|讓從上一次認可或復原後的所有變更成為永久狀態，並且釋放目前由這個 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 物件保留的任何資料庫鎖定。|  
|[createBlob](../../../connect/jdbc/reference/createblob-method-sqlserverconnection.md)|建立不包含任何資料的 **java.sql.Blob** 物件。|  
|[createClob](../../../connect/jdbc/reference/createclob-method-sqlserverconnection.md)|建立不包含任何資料的 **java.sql.Clob** 物件。|  
|[createNClob](../../../connect/jdbc/reference/createnclob-method-sqlserverconnection.md)|建立不包含任何資料的 **java.sql.NClob** 物件。|  
|[createStatement](../../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md)|建立 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 物件，以便將 SQL 陳述式傳送至資料庫。|  
|[createSQLXML](../../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md)|建立不包含任何資料的 **java.sql.SQLXML** 物件。|  
|[getAutoCommit](../../../connect/jdbc/reference/getautocommit-method-sqlserverconnection.md)|擷取這個 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 物件的目前自動認可模式。|  
|[getCatalog](../../../connect/jdbc/reference/getcatalog-method-sqlserverconnection.md)|擷取這個 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 物件的目前目錄名稱。|  
|[getClientConnectionID 方法 &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/getclientconnectionid-method-sqlserverconnection.md)|取得最新連接嘗試的連接識別碼，不論嘗試成功或失敗。|  
|[getClientInfo](../../../connect/jdbc/reference/getclientinfo-method-sqlserverconnection.md)|擷取有關 JDBC 驅動程式所支援之用戶端資訊屬性的資訊。|  
|[getDisableStatementPooling](../../../connect/jdbc/reference/getdisablestatementpooling-method-sqlserverconnection.md)|傳回 **disableStatementPooling** 連接屬性的值。 此設定控制陳述式共用是否已針對此連線啟用。|
|[getDiscardedServerPreparedStatementCount](../../../connect/jdbc/reference/getdiscardedserverpreparedstatementcount-method-sqlserverconnection.md)|傳回目前未完成備妥陳述式未準備動作的數目。|
|[getEnablePrepareOnFirstPreparedStatementCall](../../../connect/jdbc/reference/getenableprepareonfirstpreparedstatementcall-method-sqlserverconnection.md)|傳回 **enablePrepareOnFirstPreparedStatementCall** 連接屬性的值。|
|[getHoldability](../../../connect/jdbc/reference/getholdability-method-sqlserverconnection.md)|擷取 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件的目前保留性，這些物件是使用此 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 物件所建立。|  
|[getMetaData](../../../connect/jdbc/reference/getmetadata-method-sqlserverconnection.md)|擷取 [SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) 物件，其中包含此 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 物件表示連接到其中資料庫的相關中繼資料。|  
|[getServerPreparedStatementDiscardThreshold](../../../connect/jdbc/reference/getserverpreparedstatementdiscardthreshold-method-sqlserverconnection.md)|傳回 **serverPreparedStatementDiscardThreshold** 連接屬性的值。|  
|[getStatementHandleCacheEntryCount](../../../connect/jdbc/reference/getstatementhandlecacheentrycount-method-sqlserverconnection.md)|傳回目前共用備妥陳述式控制代碼的數目。|  
|[getStatementPoolingCacheSize](../../../connect/jdbc/reference/getstatementpoolingcachesize-method-sqlserverconnection.md)|傳回此連線備妥陳述式快取的大小。|  
|[getTransactionIsolation](../../../connect/jdbc/reference/gettransactionisolation-method-sqlserverconnection.md)|擷取這個 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 物件的目前交易隔離等級。|  
|[getTypeMap](../../../connect/jdbc/reference/gettypemap-method-sqlserverconnection.md)|擷取與這個 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 物件建立關聯的 Map 物件。|  
|[getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverconnection.md)|擷取由呼叫這個 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 物件所報告的第一個警告。|  
|[isClosed](../../../connect/jdbc/reference/isclosed-method-sqlserverconnection.md)|指出這個 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 物件是否已關閉。|  
|[isReadOnly](../../../connect/jdbc/reference/isreadonly-method-sqlserverconnection.md)|指出這個 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 物件是否處於唯讀模式。|  
|[isStatementPoolingEnabled](../../../connect/jdbc/reference/isstatementpoolingenabled-method-sqlserverconnection.md)|傳回陳述式共用是否已針對此連線啟用。|  
|[isValid](../../../connect/jdbc/reference/isvalid-method-sqlserverconnection.md)|指出這個 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 物件是否尚未關閉，而且仍然有效。|  
|[nativeSQL](../../../connect/jdbc/reference/nativesql-method-sqlserverconnection.md)|將給定的 SQL 陳述式轉換成資料庫伺服器的原生 SQL 文法。|  
|[prepareCall](../../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md)|建立 [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md) 物件，以便呼叫資料庫預存程序。|  
|[prepareStatement](../../../connect/jdbc/reference/preparestatement-method-sqlserverconnection.md)|建立 [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 物件，以便將參數化 SQL 陳述式傳送至資料庫。|  
|[releaseSavepoint](../../../connect/jdbc/reference/releasesavepoint-method-sqlserverconnection.md)|從目前的交易，移除指定的 [SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md) 物件。|  
|[rollback](../../../connect/jdbc/reference/rollback-method-sqlserverconnection.md)|復原目前交易中所做的所有變更，並釋放目前由這個 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 物件保留的所有資料庫鎖定。|  
|[setAutoCommit](../../../connect/jdbc/reference/setautocommit-method-sqlserverconnection.md)|將這個 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 物件的自動認可模式設定為所指定狀態。|  
|[setCatalog](../../../connect/jdbc/reference/setcatalog-method-sqlserverconnection.md)|設定指定的目錄名稱，以便選取這個 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 物件的資料庫子空間，也就是要用來工作的空間。|  
|[setClientInfo](../../../connect/jdbc/reference/setclientinfo-method-sqlserverconnection.md)|設定用戶端資訊屬性的值。|  
|[setDisableStatementPooling](../../../connect/jdbc/reference/setdisablestatementpooling-method-sqlserverconnection.md)|將陳述式共用設定為 true 或 false。|  
|[setEnablePrepareOnFirstPreparedStatementCall](../../../connect/jdbc/reference/setenableprepareonfirstpreparedstatementcall-method-sqlserverconnection.md)|指定 **enablePrepareOnFirstPreparedStatementCall** 連接屬性的新值。|  
|[setHoldability](../../../connect/jdbc/reference/setholdability-method-sqlserverconnection.md)|變更 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件保留性成為指定的保留性，這些物件是使用此 [SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md) 物件所建立。|  
|[setReadOnly](../../../connect/jdbc/reference/setreadonly-method-sqlserverconnection.md)|切換這個 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 物件成為唯讀模式，當作 JDBC 驅動程式啟用資料庫最佳化的提示。|  
|[setSavepoint](../../../connect/jdbc/reference/setsavepoint-method-sqlserverconnection.md)|在目前交易中建立未命名的儲存點，並傳回表示該儲存點的新 [SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md) 物件。|  
|[setServerPreparedStatementDiscardThreshold](../../../connect/jdbc/reference/setserverpreparedstatementdiscardthreshold-method-sqlserverconnection.md)|設定 **serverPreparedStatementDiscardThreshold** 連接屬性的新值。|  
|[setStatementPoolingCacheSize](../../../connect/jdbc/reference/setstatementpoolingcachesize-method-sqlserverconnection.md)|針對此連線設定備妥陳述式快取的大小。|  
|[setTransactionIsolation](../../../connect/jdbc/reference/settransactionisolation-method-sqlserverconnection.md)|嘗試將這個 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 物件的交易隔離等級變更為所指定等級。|  
|[setTypeMap](../../../connect/jdbc/reference/settypemap-method-sqlserverconnection.md)|安裝所指定 TypeMap object 物件來作為這個 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 物件的類型對應。|  
  
## <a name="inherited-methods"></a>繼承的方法  
  
|類別繼承自：|方法|  
|---------------------------|-------------|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.lang.Wrapper|isWrapperFor, unwrap|  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
