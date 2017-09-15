---
title: "SQLServerCallableStatement 成員 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apitype: Assembly
ms.assetid: 5ebdc186-e50f-4d14-bbf4-95af5051e4a4
caps.latest.revision: 50
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 430675118dcccfbeb93c33c936b674daee8403c9
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlservercallablestatement-members"></a>SQLServerCallableStatement 成員
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  下表列出所公開的成員[SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)類別。  
  
## <a name="constructors"></a>建構函式  
 無。  
  
## <a name="fields"></a>欄位  
  
|類別繼承自：|方法|  
|---------------------------|-------------|  
|java.sql.Statement|CLOSE_ALL_RESULTS, CLOSE_CURRENT_RESULT, EXECUTE_FAILED, KEEP_CURRENT_RESULT, NO_GENERATED_KEYS, RETURN_GENERATED_KEYS, SUCCESS_NO_INFO|  
  
## <a name="inherited-fields"></a>繼承的欄位  
 無。  
  
## <a name="methods"></a>方法  
  
|名稱|Description|  
|----------|-----------------|  
|[addBatch](../../../connect/jdbc/reference/addbatch-method-sqlserverpreparedstatement.md)|(繼承自[SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)。)將一組參數加入至這個 CallableStatement 物件的命令批次。|  
|[[取消]](../../../connect/jdbc/reference/cancel-method-sqlserverstatement.md)|(繼承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)取消目前正由這個 CallableStatement 物件執行的 SQL 陳述式。|  
|[clearBatch](../../../connect/jdbc/reference/clearbatch-method-sqlserverpreparedstatement.md)|(繼承自[SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)。)清空目前這個 CallableStatement 物件的 SQL 命令的清單。|  
|[clearParameters](../../../connect/jdbc/reference/clearparameters-method-sqlserverpreparedstatement.md)|(繼承自[SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)。)立刻清除目前的參數值。|  
|[clearWarnings](../../../connect/jdbc/reference/clearwarnings-method-sqlserverstatement.md)|(繼承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)清除此 CallableStatement 物件所報告的所有警告。|  
|[關閉](../../../connect/jdbc/reference/close-method-sqlserverpreparedstatement.md)|(繼承自[SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)。)釋出資料庫和 JDBC 資源，立即而非等待它們由系統自動釋放這個 CallableStatement 物件。|  
|[執行](../../../connect/jdbc/reference/execute-method-sqlserverpreparedstatement.md)|(繼承自[SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)。)在這個 CallableStatement 物件，它可以是任何一種 SQL 陳述式中執行的 SQL 陳述式。|  
|[executeBatch](../../../connect/jdbc/reference/executebatch-method-sqlserverpreparedstatement.md)|(繼承自[SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)。)將命令批次提交到要執行的資料庫。 如果所有命令都成功執行，則傳回更新計數陣列。|  
|[executeQuery](../../../connect/jdbc/reference/executequery-method-sqlserverpreparedstatement.md)|(繼承自[SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)。)在這個 CallableStatement 物件中執行 SQL 查詢，並傳回[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)查詢所產生的物件。|  
|[executeUpdate](../../../connect/jdbc/reference/executeupdate-method-sqlserverpreparedstatement.md)|(繼承自[SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)。)執行 SQL 陳述式中必須是 SQL INSERT、 UPDATE、 MERGE 或 DELETE 陳述式; 這個 CallableStatement 物件或不傳回任何東西，例如 DDL 陳述式的 SQL 陳述式。|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverstatement.md)|(繼承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)擷取[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)產生這個 CallableStatement 物件的物件。|  
|[getDateTimeOffset](../../../connect/jdbc/reference/getdatetimeoffset-method-sqlservercallablestatement.md)|擷取所指定的資料行的值[DateTimeOffset 類別](../../../connect/jdbc/reference/datetimeoffset-class.md)物件。|  
|[getFetchDirection](../../../connect/jdbc/reference/getfetchdirection-method-sqlserverstatement.md)|(繼承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)擷取從資料庫資料表擷取資料列的方向是從這個 CallableStatement 物件產生的結果集的預設值。|  
|[getFetchSize](../../../connect/jdbc/reference/getfetchsize-method-sqlserverstatement.md)|(繼承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)擷取的結果集資料列數目，顯示為結果的預設提取大小設定從這個 CallableStatement 物件產生的物件。|  
|[getGeneratedKeys](../../../connect/jdbc/reference/getgeneratedkeys-method-sqlserverstatement.md)|(繼承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)擷取執行這個 CallableStatement 物件最後所建立之任何自動產生索引鍵。|  
|[getMaxFieldSize](../../../connect/jdbc/reference/getmaxfieldsize-method-sqlserverstatement.md)|(繼承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)擷取最大可傳回的字元和二進位資料行中的值的位元組數[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)這個 CallableStatement 物件所產生的物件。|  
|[getMaxRows](../../../connect/jdbc/reference/getmaxrows-method-sqlserverstatement.md)|(繼承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)擷取資料列數目上限， [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)這個 CallableStatement 物件所產生的物件可以包含。|  
|[getMetaData](../../../connect/jdbc/reference/getmetadata-method-sqlserverpreparedstatement.md)|(繼承自[SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)。)擷取[SQLServerResultSetMetaData 類別](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)物件，其中包含有關的資料行資訊[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)執行這個 CallableStatement 物件時，會傳回的物件。|  
|[getMoreResults](../../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md)|(繼承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)移至這個 CallableStatement 物件的下一個結果。|  
|[getParameterMetaData](../../../connect/jdbc/reference/getparametermetadata-method-sqlserverpreparedstatement.md)|(繼承自[SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)。)擷取數字、 類型和屬性，這個 CallableStatement 物件的參數。|  
|[getArray](../../../connect/jdbc/reference/getarray-method-sqlservercallablestatement.md)|擷取指定之參數的值來當做陣列物件。|  
|[getAsciiStream](../../../connect/jdbc/reference/getasciistream-method-sqlservercallablestatement.md)|擷取指定參數的值來當做資料流**ASCII**字元。|  
|[getBigDecimal](../../../connect/jdbc/reference/getbigdecimal-method-sqlservercallablestatement.md)|擷取指定之參數的值來當做 java.math.BigDecimal。|  
|[getBinaryStream](../../../connect/jdbc/reference/getbinarystream-method-sqlservercallablestatement.md)|擷取指定之參數的值來當做不中斷位元組的二進位資料流。|  
|[getBlob](../../../connect/jdbc/reference/getblob-method-sqlservercallablestatement.md)|擷取指定之 JDBC Blob 參數的值來當做 Blob 物件使用 Java 程式語言。|  
|[getboolean](../../../connect/jdbc/reference/getboolean-method-sqlservercallablestatement.md)|擷取所指定之參數的值**布林**值。|  
|[getByte](../../../connect/jdbc/reference/getbyte-method-sqlservercallablestatement.md)|擷取所指定之參數的值**位元組**值。|  
|[getBytes](../../../connect/jdbc/reference/getbytes-method-sqlservercallablestatement.md)|擷取指定之參數的值來當做位元組陣列。|  
|[getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlservercallablestatement.md)|擷取指定之參數的值來當做 java.io.Reader 物件。|  
|[getClob](../../../connect/jdbc/reference/getclob-method-sqlservercallablestatement.md)|Clob 中的物件使用 Java 程式語言，擷取指定之 JDBC Blob 參數的值。|  
|[getDate](../../../connect/jdbc/reference/getdate-method-sqlservercallablestatement.md)|使用 Java 程式語言，擷取指定之參數的值來當做 java.sql.Date 物件。|  
|[getDateTimeOffset](../../../connect/jdbc/reference/getdatetimeoffset-method-sqlservercallablestatement.md)|擷取所指定的資料行的值[DateTimeOffset 類別](../../../connect/jdbc/reference/datetimeoffset-class.md)物件。|  
|[getDouble](../../../connect/jdbc/reference/getdouble-method-sqlservercallablestatement.md)|擷取所指定之參數的值**double**在 Java 程式語言。|  
|[getFloat](../../../connect/jdbc/reference/getfloat-method-sqlservercallablestatement.md)|擷取所指定之參數的值**float**在 Java 程式語言。|  
|[getInt](../../../connect/jdbc/reference/getint-method-sqlservercallablestatement.md)|擷取所指定之參數的值**int**在 Java 程式語言。|  
|[getLong](../../../connect/jdbc/reference/getlong-method-sqlservercallablestatement.md)|擷取所指定之參數的值**長**在 Java 程式語言。|  
|[getNCharacterStream](../../../connect/jdbc/reference/getncharacterstream-method-sqlservercallablestatement.md)|擷取指定之參數的值為讀取器物件。|  
|[getNClob](../../../connect/jdbc/reference/getnclob-method-sqlservercallablestatement.md)|擷取指定之 JDBC 值**NCLOB**參數做為**NClob** Java 程式語言中的物件。|  
|[getNString](../../../connect/jdbc/reference/getnstring-method-sqlservercallablestatement.md)|擷取值，指定**NCHAR**， **NVARCHAR**或**LONGNVARCHAR**參數做為在 Java 程式語言的字串。|  
|[getObject](../../../connect/jdbc/reference/getobject-method-sqlservercallablestatement.md)|使用 Java 程式語言，擷取指定之參數的值來當做物件。|  
|[getQueryTimeout](../../../connect/jdbc/reference/getquerytimeout-method-sqlserverstatement.md)|(繼承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)擷取秒數[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]將等候這個 CallableStatement 物件執行。|  
|[getRef](../../../connect/jdbc/reference/getref-method-sqlservercallablestatement.md)|擷取指定之參數的值來當做 Java 程式語言 Ref 物件。|  
|[getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md)|(繼承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)擷取的回應緩衝模式，這個[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)物件。|  
|[getResultSet](../../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md)|(繼承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)擷取目前結果當做[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。|  
|[getResultSetConcurrency](../../../connect/jdbc/reference/getresultsetconcurrency-method-sqlserverstatement.md)|(繼承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)擷取結果集並行[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)這個 CallableStatement 物件所產生的物件。|  
|[getResultSetHoldability](../../../connect/jdbc/reference/getresultsetholdability-method-sqlserverstatement.md)|(繼承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)擷取結果集保留性[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)這個 CallableStatement 物件所產生的物件。|  
|[getResultSetType](../../../connect/jdbc/reference/getresultsettype-method-sqlserverstatement.md)|(繼承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)擷取結果集類型為[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)這個 CallableStatement 物件所產生的物件。|  
|[getShort](../../../connect/jdbc/reference/getshort-method-sqlservercallablestatement.md)|擷取所指定之參數的值**簡短**在 Java 程式語言。|  
|[getString](../../../connect/jdbc/reference/getstring-method-sqlservercallablestatement.md)|擷取所指定之參數的值**字串**在 Java 程式語言。|  
|[getSQLXML](../../../connect/jdbc/reference/getsqlxml-method-sqlservercallablestatement.md)|擷取指定參數的值來當做 java.sql.SQLXML 物件。|  
|[getTime](../../../connect/jdbc/reference/gettime-method-sqlservercallablestatement.md)|使用 Java 程式語言，擷取指定之參數的值來當做 java.sql.Time 物件。|  
|[getTimestamp](../../../connect/jdbc/reference/gettimestamp-method-sqlservercallablestatement.md)|使用 Java 程式語言，擷取指定之參數的值來當做 java.sql.Timestamp 物件。|  
|[getUpdateCount](../../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md)|(繼承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)擷取目前結果當做更新計數。|  
|[getURL](../../../connect/jdbc/reference/geturl-method-sqlservercallablestatement.md)|URL 中的物件使用 Java 程式語言，擷取指定之參數的值。|  
|[getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverstatement.md)|(繼承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)擷取由呼叫這個 CallableStatement 物件所報告的第一個警告。|  
|[isClosed](../../../connect/jdbc/reference/isclosed-method-sqlserverstatement.md)|(繼承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)指出是否已關閉這個陳述式物件。|  
|[isPoolable](../../../connect/jdbc/reference/ispoolable-method-sqlserverstatement.md)|(繼承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)傳回值，這個值指出陳述式是否可以加入至使用者提供的陳述式集區。|  
|[isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlservercallablestatement.md)|指出這個陳述式物件是否為指定之介面的包裝函式。|  
|[registerOutParameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md)|註冊 OUT 參數。|  
|[setArray](../../../connect/jdbc/reference/setarray-method-sqlserverpreparedstatement.md)|(繼承自[SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)。)將指定的參數編號設定為指定的陣列物件。|  
|[setAsciiStream](../../../connect/jdbc/reference/setasciistream-sqlservercallablestatement.md)|設定指定的參數為給定的輸入資料流。|  
|[setBigDecimal](../../../connect/jdbc/reference/setbigdecimal-method-sqlservercallablestatement.md)|將指定的參數編號設定為給定的 BigDecimal 物件。|  
|[setBinaryStream](../../../connect/jdbc/reference/setbinarystream-sqlservercallablestatement.md)|將指定的參數設定為指定的輸入資料流。|  
|[setBlob](../../../connect/jdbc/reference/setblob-method-sqlserverpreparedstatement.md)|(繼承自[SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)。)指定的參數設定為給定的 Blob 物件。|  
|[setboolean](../../../connect/jdbc/reference/setboolean-method-sqlservercallablestatement.md)|將指定的參數設定為給定**布林**值。|  
|[setByte](../../../connect/jdbc/reference/setbyte-method-sqlservercallablestatement.md)|將指定的參數設定為給定**位元組**值。|  
|[setBytes](../../../connect/jdbc/reference/setbytes-method-sqlservercallablestatement.md)|指定的參數設定為指定的陣列**位元組**值。|  
|[setCharacterStream](../../../connect/jdbc/reference/setcharacterstream-method-sqlservercallablestatement.md)|指定的參數設定為給定的讀取器物件。|  
|[setClob](../../../connect/jdbc/reference/setclob-method-sqlservercallablestatement.md)|(繼承自[SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)。)將指定的參數設定為指定的物件。|  
|[setCursorName](../../../connect/jdbc/reference/setcursorname-method-sqlserverstatement.md)|(繼承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)將 SQL 資料指標名稱設定為給定的字串，此字串將由後續 execute 方法使用。|  
|[setDate](../../../connect/jdbc/reference/setdate-method-sqlservercallablestatement.md)|將指定的參數設定為給定的日期值。|  
|[setDateTimeOffset](../../../connect/jdbc/reference/setdatetimeoffset-method-sqlservercallablestatement.md)|設定指定的資料行的值[DateTimeOffset 類別](../../../connect/jdbc/reference/datetimeoffset-class.md)值。|  
|[setDouble](../../../connect/jdbc/reference/setdouble-method-sqlservercallablestatement.md)|將指定的參數設定為給定**double**值。|  
|[setEscapeProcessing](../../../connect/jdbc/reference/setescapeprocessing-method-sqlserverstatement.md)|(繼承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)設定逸出處理模式。|  
|[setFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverstatement.md)|(繼承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)提供 JDBC Driver 提示，當做處理結果集資料列時應遵循的方向。|  
|[setFetchSize](../../../connect/jdbc/reference/setfetchsize-method-sqlserverstatement.md)|(繼承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)提供 JDBC Driver 提示，當做在需要更多資料列時應該從資料庫中提取的資料列數目。|  
|[setFloat](../../../connect/jdbc/reference/setfloat-method-sqlservercallablestatement.md)|指定的參數設定為指定**float**值。|  
|[setInt](../../../connect/jdbc/reference/setint-method-sqlservercallablestatement.md)|指定的參數設定為指定**int**值。|  
|[setLong](../../../connect/jdbc/reference/setlong-method-sqlservercallablestatement.md)|指定的參數設定為指定**長**值。|  
|[setMaxFieldSize](../../../connect/jdbc/reference/setmaxfieldsize-method-sqlserverstatement.md)|(繼承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)設定中的位元組數目上限限制[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)資料行儲存字元或二進位值，以指定的位元組數目。|  
|[setMaxRows](../../../connect/jdbc/reference/setmaxrows-method-sqlserverstatement.md)|(繼承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)任何設定的資料列數目上限限制[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件可以包含指定的數字。|  
|[setNCharacterStream](../../../connect/jdbc/reference/setncharacterstream-method-sqlservercallablestatement.md)|將指定之的參數設定為指定的讀取器物件。|  
|[setNClob](../../../connect/jdbc/reference/setnclob-method-sqlservercallablestatement.md)|將指定的參數設定為指定的物件。|  
|[setNString](../../../connect/jdbc/reference/setnstring-method-sqlservercallablestatement.md)|將指定的參數設定為指定的字串物件。|  
|[setNull](../../../connect/jdbc/reference/setnull-method-sqlservercallablestatement.md)|在給定要設定之參數的類型時，將指定的參數設定為 null 值。|  
|[setObject](../../../connect/jdbc/reference/setobject-method-sqlservercallablestatement.md)|使用給定物件，設定指定之參數的值。|  
|[setPoolable](../../../connect/jdbc/reference/setpoolable-method-sqlserverstatement.md)|(繼承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)要求共用或不共用陳述式。 根據預設，SQLServerCallableStatement 物件時它是建立。|  
|[setQueryTimeout](../../../connect/jdbc/reference/setquerytimeout-method-sqlserverstatement.md)|(繼承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)設定驅動程式將等候 CallableStatement 物件執行指定的秒數的秒數。|  
|[setRef](../../../connect/jdbc/reference/setref-method-sqlserverpreparedstatement.md)|(繼承自[SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)。)設定指定的參數，指定參考的物件。|  
|[setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)|(繼承自[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)。)設定的回應緩衝模式，這個[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)物件以不區分大小寫**完整字串**或**適應性**。|  
|[setShort](../../../connect/jdbc/reference/setshort-method-sqlservercallablestatement.md)|指定的參數設定為指定**簡短**值。|  
|[setString](../../../connect/jdbc/reference/setstring-method-sqlservercallablestatement.md)|將指定的參數設定為指定的 Java**字串**值。|  
|[setSQLXML](../../../connect/jdbc/reference/setsqlxml-method-sqlservercallablestatement.md)|指定的參數設定為指定**SQLXML**物件。|  
|[setTime](../../../connect/jdbc/reference/settime-method-sqlservercallablestatement.md)|設定指定的參數為指定的 time 值。|  
|[setTimestamp](../../../connect/jdbc/reference/settimestamp-method-sqlservercallablestatement.md)|設定指定的參數為指定的 timestamp 值。|  
|[setUnicodeStream](../../../connect/jdbc/reference/setunicodestream-method-sqlserverpreparedstatement.md)|(繼承自[SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)。)設定指定的參數數值為給定的輸入資料流，其中將包含指定的位元組數目。|  
|[setURL](../../../connect/jdbc/reference/seturl-method-sqlservercallablestatement.md)|設定指定的參數為指定的 URL 值。|  
|[解除包裝](../../../connect/jdbc/reference/unwrap-method-sqlservercallablestatement.md)|傳回物件，用於實作指定的介面，以允許存取[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]-特有的方法。|  
|[wasNull](../../../connect/jdbc/reference/wasnull-method-sqlservercallablestatement.md)|擷取值，此值指出上一個讀取的 OUT 參數是否包含值 SQL NULL。|  
  
## <a name="inherited-methods"></a>繼承的方法  
  
|類別繼承自：|方法|  
|---------------------------|-------------|  
|com.microsoft.sqlserver.jdbc.SQLServerPreparedStatement|addBatch, clearBatch, clearParameters, close, execute, executeBatch, executeQuery, executeUpdate, getMetaData, getParameterMetaData, setArray, setAsciiStream, setBigDecimal, setBinaryStream, setBlob, setboolean, setByte, setBytes, setCharacterStream, setClob, setDate, setDouble, setFloat, setInt, setLong, setNull, setObject, setRef, setShort, setString, setTime, setTimestamp, setUnicodeStream, setURL|  
|com.microsoft.sqlserver.jdbc.SQLServerStatement|cancel, clearWarnings, execute, executeUpdate, getConnection, getFetchDirection, getFetchSize, getGeneratedKeys, getMaxFieldSize, getMaxRows, getMoreResults, getQueryTimeout, getResultSet, getResultSetConcurrency, getResultSetHoldability, getResultSetType, getUpdateCount, getWarnings, isPoolable, setCursorName, setEscapeProcessing, setFetchDirection, setFetchSize, setMaxFieldSize, setMaxRows, setPoolable, setQueryTimeout|  
|class java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait,|  
|java.sql.PreparedStatement|addBatch, clearParameters, execute, executeQuery, executeUpdate, getMetaData, getParameterMetaData, getSQLXML, setArray, setAsciiStream, setBigDecimal, setBinaryStream, setBlob, setboolean, setByte, setBytes, setCharacterStream, setClob, setDate, setDate, setDouble, setFloat, setInt, setLong, setNull, setObject, setRef, setShort, setString, setSQLXML, setTime, setTimestamp, setUnicodeStream, setURL|  
|java.sql.Statement|addBatch, cancel, clearBatch, clearWarnings, close, execute, executeBatch, executeQuery, executeUpdate, getConnection, getFetchDirection, getFetchSize, getGeneratedKeys, getMaxFieldSize, getMaxRows, getMoreResults, getQueryTimeout, getResultSet, getResultSetConcurrency, getResultSetHoldability, getResultSetType, getUpdateCount, getWarnings, setCursorName, setEscapeProcessing, setFetchDirection, setFetchSize, setMaxFieldSize, setMaxRows, setQueryTimeout|  
|java.sql.Wrapper|isWrapperFor, unwrap|  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
