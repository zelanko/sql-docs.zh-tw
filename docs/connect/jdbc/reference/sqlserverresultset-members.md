---
title: SQLServerResultSet 成員 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
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
ms.assetid: 2a438d5d-2d6a-46a0-a2ae-f35fbae4a472
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 610ace1ea15f69277cba1e4bd37b365a2c3e1cc9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sqlserverresultset-members"></a>SQLServerResultSet 成員
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  下表列出所公開的成員[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)類別。  
  
## <a name="constructors"></a>建構函式  
 無。  
  
## <a name="fields"></a>欄位  
  
|名稱|Description|  
|----------|-----------------|  
|[CONCUR_SS_OPTIMISTIC_CC](../../../connect/jdbc/reference/concur-ss-optimistic-cc-field-sqlserverresultset.md)|用來指定[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]讀取/寫入開放式並行類型沒有任何資料列鎖定。|  
|[CONCUR_SS_OPTIMISTIC_CCVAL](../../../connect/jdbc/reference/concur-ss-optimistic-ccval-field-sqlserverresultset.md)|用來指定[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]讀取/寫入開放式並行類型沒有任何資料列鎖定。|  
|[CONCUR_SS_SCROLL_LOCKS](../../../connect/jdbc/reference/concur-ss-scroll-locks-field-sqlserverresultset.md)|用來指定[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]讀取/寫入開放式並行類型的資料列鎖定。|  
|[TYPE_SS_DIRECT_FORWARD_ONLY](../../../connect/jdbc/reference/type-ss-direct-forward-only-field-sqlserverresultset.md)|用來指定[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]快速順向、 唯讀資料指標類型。|  
|[TYPE_SS_SCROLL_DYNAMIC](../../../connect/jdbc/reference/type-ss-scroll-dynamic-field-sqlserverresultset.md)|用來指定[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]動態資料指標類型。|  
|[TYPE_SS_SCROLL_KEYSET](../../../connect/jdbc/reference/type-ss-scroll-keyset-field-sqlserverresultset.md)|用來指定[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]索引鍵集資料指標類型。|  
|[TYPE_SS_SCROLL_STATIC](../../../connect/jdbc/reference/type-ss-scroll-static-field-sqlserverresultset.md)|用來指定[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]靜態資料指標類型。|  
|[TYPE_SS_SERVER_CURSOR_FORWARD_ONLY](../../../connect/jdbc/reference/type-ss-server-cursor-forward-only-field-sqlserverresultset.md)|用來指定[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]快速順向、 唯讀資料指標類型。|  
  
## <a name="inherited-fields"></a>繼承的欄位  
  
|類別繼承自：|Description|  
|---------------------------|-----------------|  
|java.sql.ResultSet|CLOSE_CURSORS_AT_COMMIT, CONCUR_READ_ONLY, CONCUR_UPDATABLE, FETCH_FORWARD, FETCH_REVERSE, FETCH_UNKNOWN, HOLD_CURSORS_OVER_COMMIT, TYPE_FORWARD_ONLY, TYPE_SCROLL_INSENSITIVE, TYPE_SCROLL_SENSITIVE|  
  
## <a name="methods"></a>方法  
  
|名稱|Description|  
|----------|-----------------|  
|[絕對](../../../connect/jdbc/reference/absolute-method-sqlserverresultset.md)|將游標移至指定的資料列，在這個[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。|  
|[afterLast](../../../connect/jdbc/reference/afterlast-method-sqlserverresultset.md)|在這最後一個資料列之後移動游標[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。|  
|[beforeFirst](../../../connect/jdbc/reference/beforefirst-method-sqlserverresultset.md)|移動至資料指標，這個第一個資料列之前[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。|  
|[cancelRowUpdates](../../../connect/jdbc/reference/cancelrowupdates-method-sqlserverresultset.md)|取消目前的資料列中所進行的更新[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。|  
|[clearWarnings](../../../connect/jdbc/reference/clearwarnings-method-sqlserverresultset.md)|清除此報告所有警告[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。|  
|[關閉](../../../connect/jdbc/reference/close-method-sqlserverresultset.md)|釋放這個[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件的資料庫和 JDBC 資源，立即而不是等待這種情形時自動關閉。|  
|[deleteRow](../../../connect/jdbc/reference/deleterow-method-sqlserverresultset.md)|刪除目前的資料列從這個[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件以及從基礎資料庫。|  
|[完成](../../../connect/jdbc/reference/finalize-method-sqlserverresultset.md)|明確地關閉此[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。|  
|[findColumn](../../../connect/jdbc/reference/findcolumn-method-sqlserverresultset.md)|擷取指定之資料行名稱在此第一個相符的資料行索引[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。|  
|[first](../../../connect/jdbc/reference/first-method-sqlserverresultset.md)|將游標移至第一個資料列，這個[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。|  
|[getArray](../../../connect/jdbc/reference/getarray-method-sqlserverresultset.md)|擷取值，這個目前的資料列中指定的資料行的[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件做為陣列物件。|  
|[getAsciiStream](../../../connect/jdbc/reference/getasciistream-method-sqlserverresultset.md)|擷取值，這個目前的資料列中指定的資料行的[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)當做 ASCII 字元資料流的物件。|  
|[getBigDecimal](../../../connect/jdbc/reference/getbigdecimal-method-sqlserverresultset.md)|擷取值，這個目前的資料列內指定之資料行索引的[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件當做 java.math.BigDecimal。|  
|[getBinaryStream](../../../connect/jdbc/reference/getbinarystream-method-sqlserverresultset.md)|擷取值，這個目前的資料列中指定的資料行的[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)當做不中斷位元組的二進位資料流的物件。|  
|[GetBlob](../../../connect/jdbc/reference/getblob-method-sqlserverresultset.md)|擷取值，這個目前的資料列中指定的資料行的[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)當做 Blob 物件在 Java 程式語言中的物件。|  
|[GetBoolean](../../../connect/jdbc/reference/getboolean-method-sqlserverresultset.md)|擷取值，這個目前的資料列中指定的資料行的[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件當做**布林**在 Java 程式語言。|  
|[GetByte](../../../connect/jdbc/reference/getbyte-method-sqlserverresultset.md)|擷取值，這個目前的資料列中指定的資料行的[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件當做**位元組**在 Java 程式語言。|  
|[GetBytes](../../../connect/jdbc/reference/getbytes-method-sqlserverresultset.md)|擷取值，這個目前的資料列中指定的資料行的[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件當做**位元組**Java 程式語言中的陣列。|  
|[getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md)|擷取值，這個目前的資料列中指定的資料行的[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件當做 java.io.Reader 物件。|  
|[getClob](../../../connect/jdbc/reference/getclob-method-sqlserverresultset.md)|擷取值，這個目前的資料列中指定的資料行的[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)當做 Java 程式語言 Clob 物件的物件。|  
|[getConcurrency](../../../connect/jdbc/reference/getconcurrency-method-sqlserverresultset.md)|擷取這個並行模式[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。|  
|[getCursorName](../../../connect/jdbc/reference/getcursorname-method-sqlserverresultset.md)|擷取 SQL 資料指標所使用的名稱[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。|  
|[getDate](../../../connect/jdbc/reference/getdate-method-sqlserverresultset.md)|擷取值，這個目前的資料列中指定的資料行的[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)來當做 java.sql.Date 物件在 Java 程式語言中的物件。|  
|[getDateTimeOffset](../../../connect/jdbc/reference/getdatetimeoffset-sqlserverresultset.md)|擷取所指定的資料行的值[DateTimeOffset 類別](../../../connect/jdbc/reference/datetimeoffset-class.md)物件。|  
|[GetDouble](../../../connect/jdbc/reference/getdouble-method-sqlserverresultset.md)|擷取值，這個目前的資料列中指定的資料行的[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件當做**double**在 Java 程式語言。|  
|[getFetchDirection](../../../connect/jdbc/reference/getfetchdirection-method-sqlserverresultset.md)|擷取這個提取方向[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。|  
|[getFetchSize](../../../connect/jdbc/reference/getfetchsize-method-sqlserverresultset.md)|擷取此提取大小[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。|  
|[GetFloat](../../../connect/jdbc/reference/getfloat-method-sqlserverresultset.md)|擷取值，這個目前的資料列中指定的資料行的[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件當做**float**在 Java 程式語言。|  
|[getHoldability](../../../connect/jdbc/reference/getholdability-method-sqlserverresultset.md)|擷取這個的保留性[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。|  
|[getInt](../../../connect/jdbc/reference/getint-method-sqlserverresultset.md)|擷取值，這個目前的資料列中指定的資料行的[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件當做**int**在 Java 程式語言。|  
|[getLong](../../../connect/jdbc/reference/getlong-method-sqlserverresultset.md)|擷取值，這個目前的資料列中指定的資料行的[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件當做**長**在 Java 程式語言。|  
|[getMetaData](../../../connect/jdbc/reference/getmetadata-method-sqlserverresultset.md)|擷取數字、 類型和屬性，這個[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件的資料行。|  
|[getNCharacterStream](../../../connect/jdbc/reference/getncharacterstream-method-sqlserverresultset.md)|擷取目前資料列內指定的資料行的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件做為讀取器物件。|  
|[getNClob](../../../connect/jdbc/reference/getnclob-method-sqlserverresultset.md)|擷取目前資料列內指定的資料行的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件當做**NClob** Java 程式語言中的物件。|  
|[getNString](../../../connect/jdbc/reference/getnstring-method-sqlserverresultset.md)|擷取目前資料列內指定的資料行的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件做為在 Java 程式語言的字串。|  
|[GetObject](../../../connect/jdbc/reference/getobject-method-sqlserverresultset.md)|取得這個目前的資料列中指定的資料行的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件為 Java 程式語言中的物件。|  
|[getRef](../../../connect/jdbc/reference/getref-method-sqlserverresultset.md)|擷取值，這個目前的資料列中指定的資料行的[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件做為參照物件，在 Java 程式語言。|  
|[getRow](../../../connect/jdbc/reference/getrow-method-sqlserverresultset.md)|擷取目前資料列數值。|  
|[getShort](../../../connect/jdbc/reference/getshort-method-sqlserverresultset.md)|擷取值，這個目前的資料列中指定的資料行的[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件當做**簡短**在 Java 程式語言。|  
|[getStatement](../../../connect/jdbc/reference/getstatement-method-sqlserverresultset.md)|擷取[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)產生此物件[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。|  
|[GetString](../../../connect/jdbc/reference/getstring-method-sqlserverresultset.md)|擷取值，這個目前的資料列中指定的資料行的[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件當做**字串**在 Java 程式語言。|  
|[getSQLXML](../../../connect/jdbc/reference/getsqlxml-method-sqlserverresultset.md)|擷取目前資料列內指定的資料行的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件當做**SQLXML**物件。|  
|[getTime](../../../connect/jdbc/reference/gettime-method-sqlserverresultset.md)|擷取值，這個目前的資料列中指定的資料行的[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)來當做 java.sql.Time 物件在 Java 程式語言中的物件。|  
|[getTimestamp](../../../connect/jdbc/reference/gettimestamp-method-sqlserverresultset.md)|擷取值，這個目前的資料列中指定的資料行的[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)來當做 java.sql.Timestamp 物件在 Java 程式語言中的物件。|  
|[GetType](../../../connect/jdbc/reference/gettype-method-sqlserverresultset.md)|擷取這個資料指標類型[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。|  
|[getUnicodeStream](../../../connect/jdbc/reference/getunicodestream-method-sqlserverresultset.md)|擷取值，這個目前的資料列中指定的資料行的[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件做為 Unicode 字元資料流。|  
|[getURL](../../../connect/jdbc/reference/geturl-method-sqlserverresultset.md)|擷取值，這個目前的資料列中指定的資料行的[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件做為 URL 物件。|  
|[getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverresultset.md)|擷取由呼叫報告上的第一個警告[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。|  
|[insertRow](../../../connect/jdbc/reference/insertrow-method-sqlserverresultset.md)|將內容插入資料列插入這[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件和資料庫。|  
|[isAfterLast](../../../connect/jdbc/reference/isafterlast-method-sqlserverresultset.md)|擷取資料指標是否在這個最後一個資料列之後[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。|  
|[isBeforeFirst](../../../connect/jdbc/reference/isbeforefirst-method-sqlserverresultset.md)|擷取值之前的第一個資料列在這個游標是否[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。|  
|[IsClosed](../../../connect/jdbc/reference/isclosed-method-sqlserverresultset.md)|指出是否此[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件已遭關閉。|  
|[isFirst](../../../connect/jdbc/reference/isfirst-method-sqlserverresultset.md)|擷取資料指標位於第一個資料列，這個值指出是否[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。|  
|[isLast](../../../connect/jdbc/reference/islast-method-sqlserverresultset.md)|擷取資料指標位於最後一個資料列，這個值指出是否[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。|  
|[最後一個](../../../connect/jdbc/reference/last-method-sqlserverresultset.md)|將游標移至最後一個資料列，在這個[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。|  
|[moveToCurrentRow](../../../connect/jdbc/reference/movetocurrentrow-method-sqlserverresultset.md)|移動資料指標到記住的資料指標位置，通常是目前資料列。|  
|[moveToInsertRow](../../../connect/jdbc/reference/movetoinsertrow-method-sqlserverresultset.md)|將資料指標移動到插入資料列。|  
|[下一步](../../../connect/jdbc/reference/next-method-sqlserverresultset.md)|從資料指標的目前位置，將資料指標向下移動到下一個資料列。|  
|[上一個](../../../connect/jdbc/reference/previous-method-sqlserverresultset.md)|將游標移至先前的資料列，在這個[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。|  
|[refreshRow](../../../connect/jdbc/reference/refreshrow-method-sqlserverresultset.md)|使用資料庫中的最新值來重新整理目前資料列。|  
|[relative](../../../connect/jdbc/reference/relative-method-sqlserverresultset.md)|移動資料游標相對於目前資料列的給定資料列數，無論是從正方向或負方向。|  
|[RowDeleted](../../../connect/jdbc/reference/rowdeleted-method-sqlserverresultset.md)|擷取值，此值指出資料列是否已遭刪除。|  
|[rowInserted](../../../connect/jdbc/reference/rowinserted-method-sqlserverresultset.md)|擷取值，此值指出目前資料列是否具有插入。|  
|[RowUpdated](../../../connect/jdbc/reference/rowupdated-method-sqlserverresultset.md)|擷取值，此值指出目前資料列是否已遭更新。|  
|[setFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverresultset.md)|提供提示，當做方向中的資料列在這個[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件將會處理。|  
|[setFetchSize](../../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md)|提供 JDBC 驅動程式提示，當做這個需要更多的資料列時應該從資料庫提取的資料列數目[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。|  
|[updateArray](../../../connect/jdbc/reference/updatearray-method-sqlserverresultset.md)|陣列物件更新指定的資料行。|  
|[updateAsciiStream](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md)|使用 ASCII 資料流值，更新指定的資料行。|  
|[updateBigDecimal](../../../connect/jdbc/reference/updatebigdecimal-method-sqlserverresultset.md)|BigDecimal 物件更新指定的資料行。|  
|[updateBinaryStream](../../../connect/jdbc/reference/updatebinarystream-method-sqlserverresultset.md)|使用二進位資料流值，更新指定的資料行。|  
|[updateBlob](../../../connect/jdbc/reference/updateblob-method-sqlserverresultset.md)|使用 java.sql.Blob 值，更新指定的資料行。|  
|[updateBoolean](../../../connect/jdbc/reference/updateboolean-method-sqlserverresultset.md)|更新指定的資料行與**布林**值。|  
|[updateByte](../../../connect/jdbc/reference/updatebyte-method-sqlserverresultset.md)|更新指定的資料行與**位元組**值。|  
|[updateBytes](../../../connect/jdbc/reference/updatebytes-method-sqlserverresultset.md)|更新指定的資料行的陣列**位元組**值。|  
|[updateCharacterStream](../../../connect/jdbc/reference/updatecharacterstream-method-sqlserverresultset.md)|使用字元資料流值，更新指定的資料行。|  
|[updateClob](../../../connect/jdbc/reference/updateclob-method-sqlserverresultset.md)|使用 java.sql.Clob 值，更新指定的資料行。|  
|[updateDate](../../../connect/jdbc/reference/updatedate-method-sqlserverresultset.md)|使用日期值，更新指定的資料行。|  
|[updateDateTimeOffset](../../../connect/jdbc/reference/updatedatetimeoffset-sqlserverresultset.md)|更新[DateTimeOffset 類別](../../../connect/jdbc/reference/datetimeoffset-class.md)資料行。|  
|[updateDouble](../../../connect/jdbc/reference/updatedouble-method-sqlserverresultset.md)|更新指定的資料行與**double**值。|  
|[updateFloat](../../../connect/jdbc/reference/updatefloat-method-sqlserverresultset.md)|更新指定的資料行與**float**值。|  
|[updateInt](../../../connect/jdbc/reference/updateint-method-sqlserverresultset.md)|更新指定的資料行與**int**值。|  
|[updateLong](../../../connect/jdbc/reference/updatelong-method-sqlserverresultset.md)|更新指定的資料行與**長**值。|  
|[updateNCharacterStream](../../../connect/jdbc/reference/updatencharacterstream-method-sqlserverresultset.md)|使用字元資料流值，更新指定的資料行。|  
|[updateNClob](../../../connect/jdbc/reference/updatenclob-method-sqlserverresultset.md)|使用指定的物件值，更新指定的資料行。|  
|[updateNString](../../../connect/jdbc/reference/updatenstring-method-sqlserverresultset.md)|更新指定的資料行與**字串**值。|  
|[updateNull](../../../connect/jdbc/reference/updatenull-method-sqlserverresultset.md)|使用 null 值，更新指定的資料行。|  
|[updateObject](../../../connect/jdbc/reference/updateobject-method-sqlserverresultset.md)|更新指定的資料行與**物件**值。|  
|[updateRef](../../../connect/jdbc/reference/updateref-method-sqlserverresultset.md)|使用 java.sql.Ref 值，更新指定的資料行。|  
|[updateRow](../../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md)|新的目前資料列，這個內容的更新基礎資料庫[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。|  
|[updateShort](../../../connect/jdbc/reference/updateshort-method-sqlserverresultset.md)|更新指定的資料行與**簡短**值。|  
|[updateString](../../../connect/jdbc/reference/updatestring-method-sqlserverresultset.md)|更新指定的資料行與**字串**值。|  
|[updateSQLXML](../../../connect/jdbc/reference/updatesqlxml-method-sqlserverresultset.md)|更新指定的資料行與**SQLXML**值。|  
|[updateTime](../../../connect/jdbc/reference/updatetime-method-sqlserverresultset.md)|使用時間值，更新指定的資料行。|  
|[updateTimestamp](../../../connect/jdbc/reference/updatetimestamp-method-sqlserverresultset.md)|使用時間戳記值，更新指定的資料行。|  
|[wasNull](../../../connect/jdbc/reference/wasnull-method-sqlserverresultset.md)|確認上一個讀取的值為 null 值。|  
  
## <a name="inherited-methods"></a>繼承的方法  
  
|類別繼承自：|方法|  
|---------------------------|-------------|  
|java.lang.Object|clone, equals, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Wrapper|isWrapperFor, unwrap|  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
