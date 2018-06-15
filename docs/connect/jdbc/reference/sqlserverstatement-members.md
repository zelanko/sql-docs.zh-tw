---
title: SQLServerStatement 成員 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 828cbaa9-ea7a-4986-95c3-5ba0d7d01d83
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 77161ec9693615eb50d4e62fb9cd1f6f185d23fe
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32853023"
---
# <a name="sqlserverstatement-members"></a>SQLServerStatement 成員
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  下表列出所公開的成員[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)類別。  
  
## <a name="constructors"></a>建構函式  
 無。  
  
## <a name="fields"></a>欄位  
 無。  
  
## <a name="inherited-fields"></a>繼承的欄位  
  
|名稱|Description|  
|----------|-----------------|  
|java.sql.Statement|CLOSE_ALL_RESULTS, CLOSE_CURRENT_RESULT, EXECUTE_FAILED, KEEP_CURRENT_RESULT, NO_GENERATED_KEYS, RETURN_GENERATED_KEYS, SUCCESS_NO_INFO|  
  
## <a name="methods"></a>方法  
  
|名稱|Description|  
|----------|-----------------|  
|[addBatch](../../../connect/jdbc/reference/addbatch-method-sqlserverstatement.md)|將給定的 SQL 命令加入至目前命令清單中，這個[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)物件。|  
|[cancel](../../../connect/jdbc/reference/cancel-method-sqlserverstatement.md)|取消目前正由此執行的 SQL 陳述式[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)物件。|  
|[clearBatch](../../../connect/jdbc/reference/clearbatch-method-sqlserverstatement.md)|清空目前的 SQL 命令清單，這個[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)物件。|  
|[clearWarnings](../../../connect/jdbc/reference/clearwarnings-method-sqlserverstatement.md)|清除所有警告，則會報告這[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)物件。|  
|[關閉](../../../connect/jdbc/reference/close-method-sqlserverstatement.md)|釋放這個[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)物件的資料庫和 JDBC 資源，立即而非等待它們由系統自動釋放。|  
|[execute](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md)|執行給定的 SQL 陳述式，此陳述式可傳回多個結果。|  
|[executeBatch](../../../connect/jdbc/reference/executebatch-method-sqlserverstatement.md)|將命令批次提交到要執行的資料庫。 如果所有命令都成功執行，則傳回更新計數陣列。|  
|[executeQuery](../../../connect/jdbc/reference/executequery-method-sqlserverstatement.md)|執行給定的 SQL 陳述式，並傳回單一[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。|  
|[executeUpdate](../../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md)|執行可能是 INSERT、UPDATE、MERGE 或 DELETE 陳述式的給定 SQL 陳述式，否則會是不傳回任何項目的 SQL 陳述式，例如 SQL DDL 陳述式。|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverstatement.md)|擷取[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)產生此物件[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)物件。|  
|[getFetchDirection](../../../connect/jdbc/reference/getfetchdirection-method-sqlserverstatement.md)|擷取從資料庫資料表擷取資料列是從這個產生的結果集的預設值的方向[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)物件。|  
|[getFetchSize](../../../connect/jdbc/reference/getfetchsize-method-sqlserverstatement.md)|擷取的結果數目集是結果集產生從這個物件的預設提取大小的資料列[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)物件。|  
|[getGeneratedKeys](../../../connect/jdbc/reference/getgeneratedkeys-method-sqlserverstatement.md)|擷取執行這個最後所建立之任何自動產生索引鍵[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)物件。|  
|[getMaxFieldSize](../../../connect/jdbc/reference/getmaxfieldsize-method-sqlserverstatement.md)|擷取最大可傳回的字元和二進位資料行中的值的位元組數[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)產生由此物件[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)物件。|  
|[getMaxRows](../../../connect/jdbc/reference/getmaxrows-method-sqlserverstatement.md)|擷取資料列數目上限， [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)產生由此物件[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)物件可以包含。|  
|[getMoreResults](../../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md)|移至下一步的結果[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)物件。|  
|[getQueryTimeout](../../../connect/jdbc/reference/getquerytimeout-method-sqlserverstatement.md)|擷取秒數[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]這將會等到[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)物件執行。|  
|[getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md)|擷取的回應緩衝模式，這個[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)物件。|  
|[getResultSet](../../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md)|擷取目前結果當做[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。|  
|[getResultSetConcurrency](../../../connect/jdbc/reference/getresultsetconcurrency-method-sqlserverstatement.md)|擷取結果集並行[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)這由所產生的物件[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)物件。|  
|[getResultSetHoldability](../../../connect/jdbc/reference/getresultsetholdability-method-sqlserverstatement.md)|擷取結果集保留性[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)這由所產生的物件[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)物件。|  
|[getResultSetType](../../../connect/jdbc/reference/getresultsettype-method-sqlserverstatement.md)|擷取結果集類型為[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)這由所產生的物件[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)物件。|  
|[getUpdateCount](../../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md)|擷取目前結果當做更新計數。|  
|[getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverstatement.md)|擷取由呼叫所報告的第一個警告[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)物件。|  
|[IsClosed](../../../connect/jdbc/reference/isclosed-method-sqlserverstatement.md)|指出是否此[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)物件已遭關閉。|  
|[isPoolable](../../../connect/jdbc/reference/ispoolable-method-sqlserverstatement.md)|傳回值，這個值指出陳述式是否可以加入至使用者提供的陳述式集區。|  
|[isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md)|指出這個陳述式物件是否為指定之介面的包裝函式。|  
|[setCursorName](../../../connect/jdbc/reference/setcursorname-method-sqlserverstatement.md)|將 SQL 資料指標名稱設定為給定的字串，此字串將由後續 execute 方法使用。|  
|[setEscapeProcessing](../../../connect/jdbc/reference/setescapeprocessing-method-sqlserverstatement.md)|設定逸出處理模式。|  
|[setFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverstatement.md)|提供 JDBC Driver 提示，當做處理結果集資料列時應遵循的方向。|  
|[setFetchSize](../../../connect/jdbc/reference/setfetchsize-method-sqlserverstatement.md)|提供 JDBC Driver 提示，當做在需要更多資料列時應該從資料庫中提取的資料列數目。|  
|[setMaxFieldSize](../../../connect/jdbc/reference/setmaxfieldsize-method-sqlserverstatement.md)|設定中的位元組數目上限限制[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)資料行儲存字元或二進位值的指定位元組數。|  
|[setMaxRows](../../../connect/jdbc/reference/setmaxrows-method-sqlserverstatement.md)|任何設定的資料列數目上限限制[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件可以包含指定的數字。|  
|[setPoolable](../../../connect/jdbc/reference/setpoolable-method-sqlserverstatement.md)|要求共用或不共用陳述式。|  
|[setQueryTimeout](../../../connect/jdbc/reference/setquerytimeout-method-sqlserverstatement.md)|設定驅動程式將等候的秒數[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)物件執行指定的秒數。|  
|[setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)|設定的回應緩衝模式，這個[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)物件以不區分大小寫**完整字串**或**適應性**。|  
|[解除包裝](../../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md)|傳回物件，用於實作指定的介面，以允許存取[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]-特有的方法。|  
  
## <a name="inherited-methods"></a>繼承的方法  
  
|類別繼承自：|方法|  
|---------------------------|-------------|  
|java.lang.Object|clone, equals, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Wrapper|isWrapperFor, unwrap|  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerStatement 類別](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
