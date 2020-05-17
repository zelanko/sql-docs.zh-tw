---
title: SQLServerResultSet 成員 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 2a438d5d-2d6a-46a0-a2ae-f35fbae4a472
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fed1b515d6e003f00cebbaf3f3a9306572e2ad2b
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "67970569"
---
# <a name="sqlserverresultset-members"></a>SQLServerResultSet 成員
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  下表列出由 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 類別公開的成員。  
  
## <a name="constructors"></a>建構函式  
 無。  
  
## <a name="fields"></a>欄位  
  
|名稱|描述|  
|----------|-----------------|  
|[CONCUR_SS_OPTIMISTIC_CC](../../../connect/jdbc/reference/concur-ss-optimistic-cc-field-sqlserverresultset.md)|用來指定不含資料列鎖定的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 讀取/寫入開放式並行類型。|  
|[CONCUR_SS_OPTIMISTIC_CCVAL](../../../connect/jdbc/reference/concur-ss-optimistic-ccval-field-sqlserverresultset.md)|用來指定不含資料列鎖定的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 讀取/寫入開放式並行類型。|  
|[CONCUR_SS_SCROLL_LOCKS](../../../connect/jdbc/reference/concur-ss-scroll-locks-field-sqlserverresultset.md)|用來指定包含資料列鎖定的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 讀取/寫入開放式並行類型。|  
|[TYPE_SS_DIRECT_FORWARD_ONLY](../../../connect/jdbc/reference/type-ss-direct-forward-only-field-sqlserverresultset.md)|用來指定 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的僅限向前快轉和唯讀等資料指標類型。|  
|[TYPE_SS_SCROLL_DYNAMIC](../../../connect/jdbc/reference/type-ss-scroll-dynamic-field-sqlserverresultset.md)|用來指定 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的動態資料指標類型。|  
|[TYPE_SS_SCROLL_KEYSET](../../../connect/jdbc/reference/type-ss-scroll-keyset-field-sqlserverresultset.md)|用來指定 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的索引鍵集資料指標類型。|  
|[TYPE_SS_SCROLL_STATIC](../../../connect/jdbc/reference/type-ss-scroll-static-field-sqlserverresultset.md)|用來指定 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的靜態資料指標類型。|  
|[TYPE_SS_SERVER_CURSOR_FORWARD_ONLY](../../../connect/jdbc/reference/type-ss-server-cursor-forward-only-field-sqlserverresultset.md)|用來指定 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的僅限向前快轉和唯讀等資料指標類型。|  
  
## <a name="inherited-fields"></a>繼承的欄位  
  
|類別繼承自：|描述|  
|---------------------------|-----------------|  
|java.sql.ResultSet|CLOSE_CURSORS_AT_COMMIT, CONCUR_READ_ONLY, CONCUR_UPDATABLE, FETCH_FORWARD, FETCH_REVERSE, FETCH_UNKNOWN, HOLD_CURSORS_OVER_COMMIT, TYPE_FORWARD_ONLY, TYPE_SCROLL_INSENSITIVE, TYPE_SCROLL_SENSITIVE|  
  
## <a name="methods"></a>方法  
  
|名稱|描述|  
|----------|-----------------|  
|[absolute](../../../connect/jdbc/reference/absolute-method-sqlserverresultset.md)|移動資料指標到這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中的指定資料列。|  
|[afterLast](../../../connect/jdbc/reference/afterlast-method-sqlserverresultset.md)|將資料指標移動到這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件的最後一個資料列的後面。|  
|[beforeFirst](../../../connect/jdbc/reference/beforefirst-method-sqlserverresultset.md)|移動資料指標到這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件第一個資料列的前面。|  
|[cancelRowUpdates](../../../connect/jdbc/reference/cancelrowupdates-method-sqlserverresultset.md)|取消對這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中目前資料列所做的更新。|  
|[clearWarnings](../../../connect/jdbc/reference/clearwarnings-method-sqlserverresultset.md)|清除這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件所報告的所有警告。|  
|[close](../../../connect/jdbc/reference/close-method-sqlserverresultset.md)|立刻釋放這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件的資料庫和 JDBC 資源，而不等待當其自動關閉時才進行釋放。|  
|[deleteRow](../../../connect/jdbc/reference/deleterow-method-sqlserverresultset.md)|從這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件和基礎資料庫中，刪除目前的資料列。|  
|[finalize](../../../connect/jdbc/reference/finalize-method-sqlserverresultset.md)|明確地關閉這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件。|  
|[findColumn](../../../connect/jdbc/reference/findcolumn-method-sqlserverresultset.md)|擷取與這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中指定資料行名稱相符合之第一個資料行的索引。|  
|[first](../../../connect/jdbc/reference/first-method-sqlserverresultset.md)|將資料指標移動到這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件的第一個資料列。|  
|[getArray](../../../connect/jdbc/reference/getarray-method-sqlserverresultset.md)|擷取這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中目前資料列中所指定資料行的值來當作陣列物件。|  
|[getAsciiStream](../../../connect/jdbc/reference/getasciistream-method-sqlserverresultset.md)|擷取這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中目前資料列中所指定資料行的值來當作 ASCII 字元資料流。|  
|[getBigDecimal](../../../connect/jdbc/reference/getbigdecimal-method-sqlserverresultset.md)|擷取這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中目前資料列中所指定資料行索引的值來當作 java.math.BigDecimal。|  
|[getBinaryStream](../../../connect/jdbc/reference/getbinarystream-method-sqlserverresultset.md)|擷取這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中目前資料列中所指定資料行的值來當作不中斷位元組的二進位資料流。|  
|[getBlob](../../../connect/jdbc/reference/getblob-method-sqlserverresultset.md)|使用 Java 程式語言，擷取這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中目前資料列中所指定資料行的值來當作 Blob 物件。|  
|[getBoolean](../../../connect/jdbc/reference/getboolean-method-sqlserverresultset.md)|使用 Java 程式語言，擷取這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中目前資料列中所指定資料行的值來當作 **Boolean**。|  
|[getByte](../../../connect/jdbc/reference/getbyte-method-sqlserverresultset.md)|使用 Java 程式語言，擷取這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中目前資料列中所指定資料行的值來當作 **byte**。|  
|[getBytes](../../../connect/jdbc/reference/getbytes-method-sqlserverresultset.md)|使用 Java 程式語言，擷取這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中目前資料列中所指定資料行的值來當作 **byte** 陣列。|  
|[getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md)|擷取這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中目前資料列中所指定資料行的值來當作 java.io.Reader 物件。|  
|[getClob](../../../connect/jdbc/reference/getclob-method-sqlserverresultset.md)|使用 Java 程式語言，擷取這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中目前資料列中所指定資料行的值來當作 Clob 物件。|  
|[getConcurrency](../../../connect/jdbc/reference/getconcurrency-method-sqlserverresultset.md)|擷取這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件的並行模式。|  
|[getCursorName](../../../connect/jdbc/reference/getcursorname-method-sqlserverresultset.md)|擷取這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件所使用 SQL 資料指標的名稱。|  
|[getDate](../../../connect/jdbc/reference/getdate-method-sqlserverresultset.md)|使用 Java 程式語言，擷取這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中目前資料列中所指定資料行的值來當作 java.sql.Date 物件。|  
|[getDateTimeOffset](../../../connect/jdbc/reference/getdatetimeoffset-sqlserverresultset.md)|擷取指定資料行的值作為 [DateTimeOffset 類別](../../../connect/jdbc/reference/datetimeoffset-class.md)物件。|  
|[getDouble](../../../connect/jdbc/reference/getdouble-method-sqlserverresultset.md)|使用 Java 程式語言，擷取這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中目前資料列中所指定資料行的值來當作 **double**。|  
|[getFetchDirection](../../../connect/jdbc/reference/getfetchdirection-method-sqlserverresultset.md)|擷取這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件的擷取方向。|  
|[getFetchSize](../../../connect/jdbc/reference/getfetchsize-method-sqlserverresultset.md)|擷取這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件的擷取大小。|  
|[getFloat](../../../connect/jdbc/reference/getfloat-method-sqlserverresultset.md)|使用 Java 程式語言，擷取這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中目前資料列中所指定資料行的值來當作 **float**。|  
|[getHoldability](../../../connect/jdbc/reference/getholdability-method-sqlserverresultset.md)|擷取這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件的保留性。|  
|[getInt](../../../connect/jdbc/reference/getint-method-sqlserverresultset.md)|使用 Java 程式語言，擷取這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中目前資料列中所指定資料行的值來當作 **int**。|  
|[getLong](../../../connect/jdbc/reference/getlong-method-sqlserverresultset.md)|使用 Java 程式語言，擷取這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中目前資料列中所指定資料行的值來當作 **long**。|  
|[getMetaData](../../../connect/jdbc/reference/getmetadata-method-sqlserverresultset.md)|擷取這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中的資料行的數字、類型和屬性。|  
|[getNCharacterStream](../../../connect/jdbc/reference/getncharacterstream-method-sqlserverresultset.md)|擷取 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中目前資料列中所指定資料行的值來當作 Reader 物件。|  
|[getNClob](../../../connect/jdbc/reference/getnclob-method-sqlserverresultset.md)|使用 Java 程式語言，擷取 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中目前資料列中所指定資料行的值來當作 **NClob** 物件。|  
|[getNString](../../../connect/jdbc/reference/getnstring-method-sqlserverresultset.md)|使用 Java 程式語言，擷取此 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中目前資料列中所指定資料行的值當作 String 物件。|  
|[getObject](../../../connect/jdbc/reference/getobject-method-sqlserverresultset.md)|使用 Java 程式語言，取得這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中目前資料列中所指定資料行的值來當作物件。|  
|[getRef](../../../connect/jdbc/reference/getref-method-sqlserverresultset.md)|使用 Java 程式語言，擷取這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中目前資料列中所指定資料行的值來當作 Ref 物件。|  
|[getRow](../../../connect/jdbc/reference/getrow-method-sqlserverresultset.md)|擷取目前資料列數值。|  
|[getShort](../../../connect/jdbc/reference/getshort-method-sqlserverresultset.md)|使用 Java 程式語言，擷取這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中目前資料列中所指定資料行的值來當作 **short**。|  
|[getStatement](../../../connect/jdbc/reference/getstatement-method-sqlserverresultset.md)|擷取產生這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverstatement-class.md) 物件的 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件。|  
|[getString](../../../connect/jdbc/reference/getstring-method-sqlserverresultset.md)|使用 Java 程式語言，擷取此 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中目前資料列中所指定資料行的值當作 **String** 物件。|  
|[getSQLXML](../../../connect/jdbc/reference/getsqlxml-method-sqlserverresultset.md)|擷取 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中目前資料列中所指定資料行的值來當作 **SQLXML** 物件。|  
|[getTime](../../../connect/jdbc/reference/gettime-method-sqlserverresultset.md)|使用 Java 程式語言，擷取這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中目前資料列中所指定資料行的值來當作 java.sql.Time 物件。|  
|[getTimestamp](../../../connect/jdbc/reference/gettimestamp-method-sqlserverresultset.md)|使用 Java 程式語言，擷取這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中目前資料列中所指定資料行的值來當作 java.sql.Timestamp 物件。|  
|[getType](../../../connect/jdbc/reference/gettype-method-sqlserverresultset.md)|擷取這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件的資料指標類型。|  
|[getUnicodeStream](../../../connect/jdbc/reference/getunicodestream-method-sqlserverresultset.md)|擷取這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中目前資料列中所指定資料行的值來當作 Unicode 字元資料流。|  
|[getURL](../../../connect/jdbc/reference/geturl-method-sqlserverresultset.md)|擷取這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中目前資料列中所指定資料行的值來當作 URL 物件。|  
|[getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverresultset.md)|擷取由呼叫這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件所報告的第一個警告。|  
|[insertRow](../../../connect/jdbc/reference/insertrow-method-sqlserverresultset.md)|將插入列的內容插入到這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件和資料庫中。|  
|[isAfterLast](../../../connect/jdbc/reference/isafterlast-method-sqlserverresultset.md)|擷取值，此值指出資料指標是否出現在這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件的最後一個資料列後面。|  
|[isBeforeFirst](../../../connect/jdbc/reference/isbeforefirst-method-sqlserverresultset.md)|擷取值，此值指出資料指標是否出現在這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件的第一個資料列前面。|  
|[isClosed](../../../connect/jdbc/reference/isclosed-method-sqlserverresultset.md)|指出這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件是否已遭關閉。|  
|[isFirst](../../../connect/jdbc/reference/isfirst-method-sqlserverresultset.md)|擷取值，此值指出資料指標是否出現在這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件的第一個資料列。|  
|[isLast](../../../connect/jdbc/reference/islast-method-sqlserverresultset.md)|擷取值，此值指出資料指標是否出現在這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件的最後一個資料列。|  
|[last](../../../connect/jdbc/reference/last-method-sqlserverresultset.md)|將資料指標移動到這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中的最後一個資料列。|  
|[moveToCurrentRow](../../../connect/jdbc/reference/movetocurrentrow-method-sqlserverresultset.md)|移動資料指標到記住的資料指標位置，通常是目前資料列。|  
|[moveToInsertRow](../../../connect/jdbc/reference/movetoinsertrow-method-sqlserverresultset.md)|將資料指標移動到插入資料列。|  
|[next](../../../connect/jdbc/reference/next-method-sqlserverresultset.md)|從資料指標的目前位置，將資料指標向下移動到下一個資料列。|  
|[previous](../../../connect/jdbc/reference/previous-method-sqlserverresultset.md)|將資料指標移動到這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中的前一個資料列。|  
|[refreshRow](../../../connect/jdbc/reference/refreshrow-method-sqlserverresultset.md)|使用資料庫中的最新值來重新整理目前資料列。|  
|[relative](../../../connect/jdbc/reference/relative-method-sqlserverresultset.md)|移動資料游標相對於目前資料列的給定資料列數，無論是從正方向或負方向。|  
|[rowDeleted](../../../connect/jdbc/reference/rowdeleted-method-sqlserverresultset.md)|擷取值，此值指出資料列是否已遭刪除。|  
|[rowInserted](../../../connect/jdbc/reference/rowinserted-method-sqlserverresultset.md)|擷取值，此值指出目前資料列是否具有插入。|  
|[rowUpdated](../../../connect/jdbc/reference/rowupdated-method-sqlserverresultset.md)|擷取值，此值指出目前資料列是否已遭更新。|  
|[setFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverresultset.md)|提供提示，作為將處理這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中資料列的方向。|  
|[setFetchSize](../../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md)|提供提示給 JDBC Driver，作為當這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件需要多個資料列時應從資料庫中提取的資料列數目。|  
|[updateArray](../../../connect/jdbc/reference/updatearray-method-sqlserverresultset.md)|使用陣列物件，更新指定的資料行。|  
|[updateAsciiStream](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md)|使用 ASCII 資料流值，更新指定的資料行。|  
|[updateBigDecimal](../../../connect/jdbc/reference/updatebigdecimal-method-sqlserverresultset.md)|使用 BigDecimal 物件來更新指定的資料行。|  
|[updateBinaryStream](../../../connect/jdbc/reference/updatebinarystream-method-sqlserverresultset.md)|使用二進位資料流值，更新指定的資料行。|  
|[updateBlob](../../../connect/jdbc/reference/updateblob-method-sqlserverresultset.md)|使用 java.sql.Blob 值，更新指定的資料行。|  
|[updateBoolean](../../../connect/jdbc/reference/updateboolean-method-sqlserverresultset.md)|使用 **boolean** 值，更新指定的資料行。|  
|[updateByte](../../../connect/jdbc/reference/updatebyte-method-sqlserverresultset.md)|使用 **byte** 值，更新指定的資料行。|  
|[updateBytes](../../../connect/jdbc/reference/updatebytes-method-sqlserverresultset.md)|使用 **byte** 值的陣列，更新指定的資料行。|  
|[updateCharacterStream](../../../connect/jdbc/reference/updatecharacterstream-method-sqlserverresultset.md)|使用字元資料流值，更新指定的資料行。|  
|[updateClob](../../../connect/jdbc/reference/updateclob-method-sqlserverresultset.md)|使用 java.sql.Clob 值，更新指定的資料行。|  
|[updateDate](../../../connect/jdbc/reference/updatedate-method-sqlserverresultset.md)|使用日期值，更新指定的資料行。|  
|[updateDateTimeOffset](../../../connect/jdbc/reference/updatedatetimeoffset-sqlserverresultset.md)|更新 [DateTimeOffset 類別](../../../connect/jdbc/reference/datetimeoffset-class.md)資料行。|  
|[updateDouble](../../../connect/jdbc/reference/updatedouble-method-sqlserverresultset.md)|使用 **double** 值，更新指定的資料行。|  
|[updateFloat](../../../connect/jdbc/reference/updatefloat-method-sqlserverresultset.md)|使用**浮點數**值，更新指定的資料行。|  
|[updateInt](../../../connect/jdbc/reference/updateint-method-sqlserverresultset.md)|使用 **int** 值，更新指定的資料行。|  
|[updateLong](../../../connect/jdbc/reference/updatelong-method-sqlserverresultset.md)|使用 **long** 值，更新指定的資料行。|  
|[updateNCharacterStream](../../../connect/jdbc/reference/updatencharacterstream-method-sqlserverresultset.md)|使用字元資料流值，更新指定的資料行。|  
|[updateNClob](../../../connect/jdbc/reference/updatenclob-method-sqlserverresultset.md)|使用指定的物件值，更新指定的資料行。|  
|[updateNString](../../../connect/jdbc/reference/updatenstring-method-sqlserverresultset.md)|使用**字串**值，更新指定的資料行。|  
|[updateNull](../../../connect/jdbc/reference/updatenull-method-sqlserverresultset.md)|使用 null 值，更新指定的資料行。|  
|[updateObject](../../../connect/jdbc/reference/updateobject-method-sqlserverresultset.md)|使用**物件**值，更新指定的資料行。|  
|[updateRef](../../../connect/jdbc/reference/updateref-method-sqlserverresultset.md)|使用 java.sql.Ref 值，更新指定的資料行。|  
|[updateRow](../../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md)|使用這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件目前資料列的新內容，更新基礎資料庫。|  
|[updateShort](../../../connect/jdbc/reference/updateshort-method-sqlserverresultset.md)|使用 **short** 值，更新指定的資料行。|  
|[updateString](../../../connect/jdbc/reference/updatestring-method-sqlserverresultset.md)|使用**字串**值，更新指定的資料行。|  
|[updateSQLXML](../../../connect/jdbc/reference/updatesqlxml-method-sqlserverresultset.md)|使用 **SQLXML** 值，更新指定的資料行。|  
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
  
  
