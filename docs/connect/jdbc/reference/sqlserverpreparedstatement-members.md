---
title: SQLServerPreparedStatement 成員 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 2363902f-d4c6-4cd4-a5fc-86079eb9e418
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9a995211f7e485971ad71a5ae290e410b8604cb0
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80925971"
---
# <a name="sqlserverpreparedstatement-members"></a>SQLServerPreparedStatement 成員
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  下表列出由 [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 類別公開的成員。  
  
## <a name="constructors"></a>建構函式  
 無。  
  
## <a name="fields"></a>欄位  
 無。  
  
## <a name="inherited-fields"></a>繼承的欄位  
  
|類別繼承自：|方法|  
|---------------------------|-------------|  
|java.sql.Statement|CLOSE_ALL_RESULTS, CLOSE_CURRENT_RESULT, EXECUTE_FAILED, KEEP_CURRENT_RESULT, NO_GENERATED_KEYS, RETURN_GENERATED_KEYS, SUCCESS_NO_INFO|  
  
## <a name="methods"></a>方法  
  
|名稱|描述|  
|----------|-----------------|  
|[addBatch](../../../connect/jdbc/reference/addbatch-method-sqlserverpreparedstatement.md)|將一組參數新增至這個 Statement 物件的批次命令中。|  
|[cancel](../../../connect/jdbc/reference/cancel-method-sqlserverstatement.md)|(繼承自 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md))。取消目前正由這個 Statement 物件執行的 SQL 陳述式。|  
|[clearBatch](../../../connect/jdbc/reference/clearbatch-method-sqlserverpreparedstatement.md)|清空這個 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 物件的 SQL 命令目前清單。|  
|[clearParameters](../../../connect/jdbc/reference/clearparameters-method-sqlserverpreparedstatement.md)|立刻清除目前的參數值。|  
|[clearWarnings](../../../connect/jdbc/reference/clearwarnings-method-sqlserverstatement.md)|(繼承自 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md))。清除這個 Statement 物件所報告的所有警告。|  
|[close](../../../connect/jdbc/reference/close-method-sqlserverpreparedstatement.md)|立刻釋放出這個 Statement 物件的資料庫和 JDBC 資源，而非等待它們由系統自動釋放。|  
|[execute](../../../connect/jdbc/reference/execute-method-sqlserverpreparedstatement.md)|在這個 Statement 物件中執行可為任何類型的 SQL 陳述式。|  
|[executeBatch](../../../connect/jdbc/reference/executebatch-method-sqlserverpreparedstatement.md)|將命令批次提交到要執行的資料庫。 如果所有命令都成功執行，則傳回更新計數陣列。|  
|[executeQuery](../../../connect/jdbc/reference/executequery-method-sqlserverpreparedstatement.md)|在這個 Statement 物件中執行 SQL 查詢，並傳回此查詢所產生的 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件。|  
|[executeUpdate](../../../connect/jdbc/reference/executeupdate-method-sqlserverpreparedstatement.md)|在這個 Statement 物件中執行必須是 SQL INSERT、UPDATE、MERGE 或 DELETE 陳述式的 SQL 陳述式，否則會是不傳回任何項目的 SQL 陳述式，例如 DDL 陳述式。|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverstatement.md)|(繼承自 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md))。擷取產生這個 Statement 物件的 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 物件。|  
|[getFetchDirection](../../../connect/jdbc/reference/getfetchdirection-method-sqlserverstatement.md)|(繼承自 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md))。擷取從資料庫資料表中提取資料列的方向，此方向是從這個 Statement 物件所產生結果集的預設值。|  
|[getFetchSize](../../../connect/jdbc/reference/getfetchsize-method-sqlserverstatement.md)|(繼承自 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md))。擷取結果集資料列數目，這個數目是從這個 Statement 物件所產生結果集物件的預設提取大小。|  
|[getGeneratedKeys](../../../connect/jdbc/reference/getgeneratedkeys-method-sqlserverstatement.md)|(繼承自 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md))。擷取執行這個 Statement 物件最後所建立的任何自動產生索引鍵。|  
|[getMaxFieldSize](../../../connect/jdbc/reference/getmaxfieldsize-method-sqlserverstatement.md)|(繼承自 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md))。擷取最大位元組數目，此位元組可傳回作為這個 Statement 物件所產生 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中的字元和二進位資料行值。|  
|[getMaxRows](../../../connect/jdbc/reference/getmaxrows-method-sqlserverstatement.md)|(繼承自 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md))。擷取最大資料列數目，即這個 Statement 物件所產生 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件可以包含的資料列。|  
|[getMetaData](../../../connect/jdbc/reference/getmetadata-method-sqlserverpreparedstatement.md)|擷取 [SQLServerResultSetMetaData 類別](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)物件，此物件包含當執行這個 Statement 物件時將傳回之 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件資料行的相關資訊。|  
|[getMoreResults](../../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md)|(繼承自 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md))。移至這個 Statement 物件的下一個結果。|  
|[getParameterMetaData](../../../connect/jdbc/reference/getparametermetadata-method-sqlserverpreparedstatement.md)|擷取這個 Statement 物件參數的號碼、類型和屬性。|  
|[getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md)|(繼承自 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md))。擷取這個 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 物件的回應緩衝模式。|  
|[getQueryTimeout](../../../connect/jdbc/reference/getquerytimeout-method-sqlserverstatement.md)|(繼承自 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md))。擷取 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 將等候這個 Statement 物件執行的秒數。|  
|[getResultSet](../../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md)|(繼承自 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md))。擷取目前結果作為 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件。|  
|[getResultSetConcurrency](../../../connect/jdbc/reference/getresultsetconcurrency-method-sqlserverstatement.md)|(繼承自 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md))。擷取由這個 Statement 物件所產生 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件的結果集並行。|  
|[getResultSetHoldability](../../../connect/jdbc/reference/getresultsetholdability-method-sqlserverstatement.md)|(繼承自 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md))。擷取由這個 Statement 物件所產生 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件的結果集保留性。|  
|[getResultSetType](../../../connect/jdbc/reference/getresultsettype-method-sqlserverstatement.md)|(繼承自 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md))。擷取由這個 Statement 物件所產生 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件的結果集類型。|  
|[getUpdateCount](../../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md)|(繼承自 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md))。擷取目前結果集作為更新計數。|  
|[getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverstatement.md)|(繼承自 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md))。擷取由呼叫這個 Statement 物件所報告的第一個警告。|  
|[isClosed](../../../connect/jdbc/reference/isclosed-method-sqlserverstatement.md)|(繼承自 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md))。指出這個 Statement 物件是否已關閉。|  
|[isPoolable](../../../connect/jdbc/reference/ispoolable-method-sqlserverstatement.md)|(繼承自 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md))。傳回值，這個值指出陳述式是否可以加入至使用者提供的陳述式集區。|  
|[isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverpreparedstatement.md)|指出這個陳述式物件是否為指定之介面的包裝函式。|  
|[setArray](../../../connect/jdbc/reference/setarray-method-sqlserverpreparedstatement.md)|將指定的參數編號設定為所指定 Array 物件。|  
|[setAsciiStream](../../../connect/jdbc/reference/setasciistream-method-sqlserverpreparedstatement.md)|將指定的參數號碼設定為所指定 InputStream 物件。|  
|[setBigDecimal](../../../connect/jdbc/reference/setbigdecimal-method-sqlserverpreparedstatement.md)|將指定的參數號碼設定為所指定 BigDecimal 物件。|  
|[setBinaryStream](../../../connect/jdbc/reference/setbinarystream-method-sqlserverpreparedstatement.md)|將指定的參數設定為指定的輸入資料流。|  
|[setBlob](../../../connect/jdbc/reference/setblob-method-sqlserverpreparedstatement.md)|將指定的參數設定為所指定 Blob 物件。|  
|[setboolean](../../../connect/jdbc/reference/setboolean-method-sqlserverpreparedstatement.md)|將指定的參數設定為所指定 **Boolean** 值。|  
|[setByte](../../../connect/jdbc/reference/setbyte-method-sqlserverpreparedstatement.md)|將指定的參數設定為所指定 **byte** 值。|  
|[setBytes](../../../connect/jdbc/reference/setbytes-method-sqlserverpreparedstatement.md)|設定指定的參數為指定的位元組陣列。|  
|[setCharacterStream](../../../connect/jdbc/reference/setcharacterstream-method-sqlserverpreparedstatement.md)|將指定的參數設定為所指定 Reader 物件。|  
|[setClob](../../../connect/jdbc/reference/setclob-method-sqlserverpreparedstatement.md)|將指定的參數設定為所指定 Clob 物件。|  
|[setCursorName](../../../connect/jdbc/reference/setcursorname-method-sqlserverstatement.md)|(繼承自 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md))。將 SQL 資料指標名稱設定為指定的字串，此字串將由後續執行方法使用。|  
|[setDate](../../../connect/jdbc/reference/setdate-method-sqlserverpreparedstatement.md)|將指定的參數設定為指定的日期值。|  
|[setDateTimeOffset](../../../connect/jdbc/reference/setdatetimeoffset-method-sqlserverpreparedstatement.md)|將指定的資料行值設定為 [DateTimeOffset 類別](../../../connect/jdbc/reference/datetimeoffset-class.md)值。|  
|[setDouble](../../../connect/jdbc/reference/setdouble-method-sqlserverpreparedstatement.md)|將指定的參數設定為所指定 **double** 值。|  
|[setEscapeProcessing](../../../connect/jdbc/reference/setescapeprocessing-method-sqlserverstatement.md)|(繼承自 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md))。設定逸出處理模式。|  
|[setFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverstatement.md)|(繼承自 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md))。提供 JDBC Driver 提示，當做處理結果集資料列時應遵循的方向。|  
|[setFetchSize](../../../connect/jdbc/reference/setfetchsize-method-sqlserverstatement.md)|(繼承自 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md))。提供 JDBC Driver 提示，當做在需要更多資料列時應該從資料庫中提取的資料列數目。|  
|[setFloat](../../../connect/jdbc/reference/setfloat-method-sqlserverpreparedstatement.md)|將指定的參數設定為所指定 **float** 值。|  
|[setInt](../../../connect/jdbc/reference/setint-method-sqlserverpreparedstatement.md)|將指定的參數設定為所指定 **int** 值。|  
|[setLong](../../../connect/jdbc/reference/setlong-method-sqlserverpreparedstatement.md)|將指定的參數設定為所指定 **long** 值。|  
|[setMaxFieldSize](../../../connect/jdbc/reference/setmaxfieldsize-method-sqlserverstatement.md)|(繼承自 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md))。將 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 資料行中用於儲存字元或二進位值的最大位元組數目限制設定為所指定位元組數目。|  
|[setMaxRows](../../../connect/jdbc/reference/setmaxrows-method-sqlserverstatement.md)|(繼承自 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md))。將任何 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件可以包含的最大資料列數目限制設定為所指定數目。|  
|[setNCharacterStream](../../../connect/jdbc/reference/setncharacterstream-method-sqlserverpreparedstatement.md)|將指定的參數設定為所指定 Reader 物件。|  
|[setNClob](../../../connect/jdbc/reference/setnclob-method-sqlserverpreparedstatement.md)|將指定的參數設定為指定的物件。|  
|[setNull](../../../connect/jdbc/reference/setnull-method-sqlserverpreparedstatement.md)|在給定要設定之參數的類型時，將指定的參數設定為 null 值。|  
|[setNString](../../../connect/jdbc/reference/setnstring-method-int-java-lang-string.md)|將指定的參數設定為所指定 **String** 物件。|  
|[setObject](../../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md)|使用給定物件，設定指定之參數的值。|  
|[setPoolable](../../../connect/jdbc/reference/setpoolable-method-sqlserverstatement.md)|(繼承自 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md))。要求共用或不共用陳述式。 根據預設，SQLServerPreparedStatement 物件在建立時是可共用的。|  
|[setQueryTimeout](../../../connect/jdbc/reference/setquerytimeout-method-sqlserverstatement.md)|(繼承自 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md))。設定驅動程式將等候這個 Statement 物件執行指定秒數的秒數。|  
|[setRef](../../../connect/jdbc/reference/setref-method-sqlserverpreparedstatement.md)|將指定的參數設定為所指定 Ref 物件。|  
|[setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)|(繼承自 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md))。將這個 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 物件的回應緩衝模式設定為 **String full** 或 **adaptive** (不區分大小寫)。|  
|[setShort](../../../connect/jdbc/reference/setshort-method-sqlserverpreparedstatement.md)|將指定的參數設定為所指定 **short** 值。|  
|[setString](../../../connect/jdbc/reference/setstring-method-sqlserverpreparedstatement.md)|將指定的參數設定為所指定 **String** 值。|  
|[setSQLXML](../../../connect/jdbc/reference/setsqlxml-method-sqlserverpreparedstatement.md)|將指定的參數設定為所指定 **SQLXML** 物件。|  
|[setTime](../../../connect/jdbc/reference/settime-method-sqlserverpreparedstatement.md)|設定指定的參數為指定的 time 值。|  
|[setTimestamp](../../../connect/jdbc/reference/settimestamp-method-sqlserverpreparedstatement.md)|設定指定的參數為指定的 timestamp 值。|  
|[setUnicodeStream](../../../connect/jdbc/reference/setunicodestream-method-sqlserverpreparedstatement.md)|設定指定的參數數值為指定的輸入資料流，其中將包含指定的位元組數目。|  
|[setURL](../../../connect/jdbc/reference/seturl-method-sqlserverpreparedstatement.md)|設定指定的參數為指定的 URL 值。|  
|[unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverpreparedstatement.md)|傳回可實作指定介面的物件，此介面可允許存取 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 特定的方法。|  
  
## <a name="inherited-methods"></a>繼承的方法  
  
|類別繼承自：|方法|  
|---------------------------|-------------|  
|com.microsoft.sqlserver.jdbc.SQLServerStatement|cancel, clearWarnings, execute, executeUpdate, getConnection, getFetchDirection, getFetchSize, getGeneratedKeys, getMaxFieldSize, getMaxRows, getMoreResults, getQueryTimeout, getResultSet, getResultSetConcurrency, getResultSetHoldability, getResultSetType, getUpdateCount, getWarnings, isPoolable, setCursorName, setEscapeProcessing, setFetchDirection, setFetchSize, setMaxFieldSize, setMaxRows, setPoolable, setQueryTimeout|  
|java.lang.Object|clone, equals, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Statement|cancel, clearWarnings, execute, executeUpdate, getConnection, getFetchDirection, getFetchSize, getGeneratedKeys, getMaxFieldSize, getMaxRows, getMoreResults, getQueryTimeout, getResultSet, getResultSetConcurrency, getResultSetHoldability, getResultSetType, getUpdateCount, getWarnings, setCursorName, setEscapeProcessing, setFetchDirection, setFetchSize, setMaxFieldSize, setMaxRows, setQueryTimeout|  
|java.sql.Wrapper|isWrapperFor, unwrap|  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerPreparedStatement 類別](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
