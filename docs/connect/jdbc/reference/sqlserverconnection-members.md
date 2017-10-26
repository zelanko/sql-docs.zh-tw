---
title: "SQLServerConnection 成員 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3115a533-756b-4c78-aee9-4ba7253c85e0
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 917a5561dd3de7f9f45434aef88bd2eb98661473
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlserverconnection-members"></a>SQLServerConnection 成員
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  下表列出所公開的成員[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)類別。  
  
## <a name="constructors"></a>建構函式  
 無。  
  
## <a name="fields"></a>欄位  
  
|名稱|Description|  
|----------|-----------------|  
|[TRANSACTION_SNAPSHOT](../../../connect/jdbc/reference/transaction-snapshot-field-sqlserverconnection.md)|用來指定快照集交易隔離等級。|  
  
## <a name="inherited-fields"></a>繼承的欄位  
  
|類別繼承自：|Description|  
|---------------------------|-----------------|  
|java.sql.Connection|TRANSACTION_NONE, TRANSACTION_READ_COMMITTED, TRANSACTION_READ_UNCOMMITTED, TRANSACTION_REPEATABLE_READ, TRANSACTION_SERIALIZABLE|  
  
## <a name="methods"></a>方法  
  
|名稱|Description|  
|----------|-----------------|  
|[clearWarnings](../../../connect/jdbc/reference/clearwarnings-method-sqlserverconnection.md)|清除這個報告所有警告[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)物件。|  
|[關閉](../../../connect/jdbc/reference/close-method-sqlserverconnection.md)|釋放這個資料庫[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)物件和 JDBC 資源，立即而非等待它們由系統自動釋放。|  
|[認可](../../../connect/jdbc/reference/commit-method-sqlserverconnection.md)|使所有變更成為上一次認可或回復之後永久狀態，並釋放由此目前保留的任何資料庫鎖定[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)物件。|  
|[createBlob](../../../connect/jdbc/reference/createblob-method-sqlserverconnection.md)|建立**java.sql.Blob**物件而不將任何資料。|  
|[createClob](../../../connect/jdbc/reference/createclob-method-sqlserverconnection.md)|建立**java.sql.Clob**物件而不將任何資料。|  
|[createNClob](../../../connect/jdbc/reference/createnclob-method-sqlserverconnection.md)|建立**java.sql.NClob**物件而不將任何資料。|  
|[createStatement](../../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md)|建立[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)物件傳送至資料庫的 SQL 陳述式。|  
|[createSQLXML](../../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md)|建立**java.sql.SQLXML**物件而不將任何資料。|  
|[getAutoCommit](../../../connect/jdbc/reference/getautocommit-method-sqlserverconnection.md)|擷取此目前自動認可模式[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)物件。|  
|[getCatalog](../../../connect/jdbc/reference/getcatalog-method-sqlserverconnection.md)|擷取目前的目錄名稱，這個[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)物件。|  
|[getClientConnectionID 方法 &#40;SQLServerConnection &#41;](../../../connect/jdbc/reference/getclientconnectionid-method-sqlserverconnection.md)|取得最新連接嘗試的連接識別碼，不論嘗試成功或失敗。|  
|[getClientInfo](../../../connect/jdbc/reference/getclientinfo-method-sqlserverconnection.md)|擷取有關 JDBC 驅動程式所支援之用戶端資訊屬性的資訊。|  
|[getHoldability](../../../connect/jdbc/reference/getholdability-method-sqlserverconnection.md)|擷取目前保留性[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)建立使用此物件[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)物件。|  
|[getMetaData](../../../connect/jdbc/reference/getmetadata-method-sqlserverconnection.md)|擷取[SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)物件，其中包含這個資料庫的相關中繼資料[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)物件代表的連接。|  
|[getTransactionIsolation](../../../connect/jdbc/reference/gettransactionisolation-method-sqlserverconnection.md)|這會擷取目前的交易隔離等級[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)物件。|  
|[getTypeMap](../../../connect/jdbc/reference/gettypemap-method-sqlserverconnection.md)|擷取與此相關聯的對應物件[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)物件。|  
|[getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverconnection.md)|擷取由呼叫報告上的第一個警告[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)物件。|  
|[isClosed](../../../connect/jdbc/reference/isclosed-method-sqlserverconnection.md)|指出是否此[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)物件已遭關閉。|  
|[isReadOnly](../../../connect/jdbc/reference/isreadonly-method-sqlserverconnection.md)|指出是否此[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)物件處於唯讀模式。|  
|[isValid](../../../connect/jdbc/reference/isvalid-method-sqlserverconnection.md)|指出是否此[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)物件尚未關閉，而且仍然有效。|  
|[nativeSQL](../../../connect/jdbc/reference/nativesql-method-sqlserverconnection.md)|將給定的 SQL 陳述式轉換成資料庫伺服器的原生 SQL 文法。|  
|[prepareCall](../../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md)|建立[SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)物件，以便呼叫資料庫預存程序。|  
|[prepareStatement](../../../connect/jdbc/reference/preparestatement-method-sqlserverconnection.md)|建立[SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)物件以傳送參數化資料庫的 SQL 陳述式。|  
|[releaseSavepoint](../../../connect/jdbc/reference/releasesavepoint-method-sqlserverconnection.md)|移除指定[SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md)物件從目前的交易。|  
|[復原](../../../connect/jdbc/reference/rollback-method-sqlserverconnection.md)|復原目前交易中所做的所有變更，並釋放目前由這個保留的任何資料庫鎖定[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)物件。|  
|[setAutoCommit](../../../connect/jdbc/reference/setautocommit-method-sqlserverconnection.md)|設定這個自動認可模式[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)處於指定狀態的物件。|  
|[setCatalog](../../../connect/jdbc/reference/setcatalog-method-sqlserverconnection.md)|設定指定的目錄名稱來選取這個子[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)中用來工作的物件的資料庫。|  
|[setClientInfo](../../../connect/jdbc/reference/setclientinfo-method-sqlserverconnection.md)|設定用戶端資訊屬性的值。|  
|[setHoldability](../../../connect/jdbc/reference/setholdability-method-sqlserverconnection.md)|變更的保留性[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)建立使用此物件[SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md)給定的保留性的物件。|  
|[setReadOnly](../../../connect/jdbc/reference/setreadonly-method-sqlserverconnection.md)|將這[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)在唯讀模式下，當做 JDBC 驅動程式，啟用資料庫最佳化提示的物件。|  
|[setSavepoint](../../../connect/jdbc/reference/setsavepoint-method-sqlserverconnection.md)|在目前交易中建立未命名的儲存點，並傳回新[SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md)物件，代表它。|  
|[setTransactionIsolation](../../../connect/jdbc/reference/settransactionisolation-method-sqlserverconnection.md)|嘗試將交易隔離等級變更這個[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)一個指定的物件。|  
|[setTypeMap](../../../connect/jdbc/reference/settypemap-method-sqlserverconnection.md)|這個安裝給定的 TypeMap 物件來當做型別對應[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)物件。|  
  
## <a name="inherited-methods"></a>繼承的方法  
  
|類別繼承自：|方法|  
|---------------------------|-------------|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.lang.Wrapper|isWrapperFor, unwrap|  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  

