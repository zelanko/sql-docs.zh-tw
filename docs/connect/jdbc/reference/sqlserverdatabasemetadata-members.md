---
title: "SQLServerDatabaseMetaData 成員 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 327ba0bc-438a-494c-b119-1cd4a096bb58
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 47a2c30638f964f04af3b4579cccbb71af1ba65c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlserverdatabasemetadata-members"></a>SQLServerDatabaseMetaData 成員
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  下表列出所公開的成員[SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)類別。  
  
## <a name="constructors"></a>建構函式  
 無。  
  
## <a name="fields"></a>欄位  
 無。  
  
## <a name="inherited-fields"></a>繼承的欄位  
  
|名稱|Description|  
|----------|-----------------|  
|java.sql.DatabaseMetaData|attributeNoNulls, attributeNullable, attributeNullableUnknown, bestRowNotPseudo, bestRowPseudo, bestRowSession, bestRowTemporary, bestRowTransaction, bestRowUnknown, columnNoNulls, columnNullable, columnNullableUnknown, importedKeyCascade, importedKeyInitiallyDeferred, importedKeyInitiallyImmediate, importedKeyNoAction, importedKeyNotDeferrable, importedKeyRestrict, importedKeySetDefault, importedKeySetNull, procedureColumnIn, procedureColumnInOut, procedureColumnOut, procedureColumnResult, procedureColumnReturn, procedureColumnUnknown, procedureNoNulls, procedureNoResult, procedureNullable, procedureNullableUnknown, procedureResultUnknown, procedureReturnsResult, sqlStateSQL, sqlStateSQL99, sqlStateXOpen, tableIndexClustered, tableIndexHashed, tableIndexOther, tableIndexStatistic, typeNoNulls, typeNullable, typeNullableUnknown, typePredBasic, typePredChar, typePredNone, typeSearchable, versionColumnNotPseudo, versionColumnPseudo, versionColumnUnknown|  
  
## <a name="methods"></a>方法  
  
|名稱|Description|  
|----------|-----------------|  
|[allProceduresAreCallable](../../../connect/jdbc/reference/allproceduresarecallable-method-sqlserverdatabasemetadata.md)|擷取目前使用者是否有權限可以呼叫所傳回的所有程序[getProcedures](../../../connect/jdbc/reference/getprocedures-method-sqlserverdatabasemetadata.md)方法。|  
|[allTablesAreSelectable](../../../connect/jdbc/reference/alltablesareselectable-method-sqlserverdatabasemetadata.md)|擷取目前使用者是否有權限來使用所傳回的所有資料表[getTables](../../../connect/jdbc/reference/gettables-method-sqlserverdatabasemetadata.md) SELECT 陳述式中的方法。|  
|[autoCommitFailureClosesAllResultSets](../../../connect/jdbc/reference/autocommitfailureclosesallresultsets-method-sqlserverdatabasemetadata.md)|指出當自動認可啟用且擲出例外狀況時，JDBC Driver 是否會關閉所有開啟的結果集，包括可保留資料的結果集。|  
|[dataDefinitionCausesTransactionCommit](../../../connect/jdbc/reference/datadefinitioncausestransactioncommit-method-sqlserverdatabasemetadata.md)|擷取值，此值指出交易中的資料定義陳述式是否會強制交易進行認可。|  
|[dataDefinitionIgnoredInTransactions](../../../connect/jdbc/reference/datadefinitionignoredintransactions-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否會忽略交易中的資料定義陳述式。|  
|[deletesAreDetected](../../../connect/jdbc/reference/deletesaredetected-method-sqlserverdatabasemetadata.md)|可以呼叫來偵測可見資料列的刪除是否擷取[rowDeleted](../../../connect/jdbc/reference/rowdeleted-method-sqlserverresultset.md)方法[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)類別。|  
|[doesMaxRowSizeIncludeBlobs](../../../connect/jdbc/reference/doesmaxrowsizeincludeblobs-method-sqlserverdatabasemetadata.md)|擷取是否傳回值[getMaxRowSize](../../../connect/jdbc/reference/getmaxrowsize-method-sqlserverdatabasemetadata.md)方法包括 SQL 資料類型 LONGVARCHAR 和 LONGVARBINARY。|  
|[getAttributes](../../../connect/jdbc/reference/getattributes-method-sqlserverdatabasemetadata.md)|擷取使用者定義類型的給定類型之給定屬性的描述，此類型可由給定結構描述和目錄提供。|  
|[getBestRowIdentifier](../../../connect/jdbc/reference/getbestrowidentifier-method-sqlserverdatabasemetadata.md)|擷取資料表中最佳資料行集的描述，此資料行集可唯一識別資料列。|  
|[getCatalogs](../../../connect/jdbc/reference/getcatalogs-method-sqlserverdatabasemetadata.md)|擷取已連接伺服器中所提供的目錄名稱。|  
|[getCatalogSeparator](../../../connect/jdbc/reference/getcatalogseparator-method-sqlserverdatabasemetadata.md)|擷取**字串**，這個資料庫會使用做為類別目錄和資料表名稱之間的分隔符號。|  
|[getCatalogTerm](../../../connect/jdbc/reference/getcatalogterm-method-sqlserverdatabasemetadata.md)|擷取資料庫供應商的慣用詞彙做為「目錄」。|  
|[getClientInfoProperties](../../../connect/jdbc/reference/getclientinfoproperties-method-sqlserverdatabasemetadata.md)|擷取此驅動程式支援之用戶端資訊屬性的清單。|  
|[getColumnPrivileges](../../../connect/jdbc/reference/getcolumnprivileges-method-sqlserverdatabasemetadata.md)|擷取資料表中資料行之存取權限的描述。|  
|[getColumns](../../../connect/jdbc/reference/getcolumns-method-sqlserverdatabasemetadata.md)|擷取可透過指定目錄提供之資料表資料行的描述。|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverdatabasemetadata.md)|擷取產生這個中繼資料物件的連接。|  
|[getCrossReference](../../../connect/jdbc/reference/getcrossreference-method-sqlserverdatabasemetadata.md)|擷取給定外部索引鍵資料表中之外部索引鍵資料行的描述，該資料表會參考給定主索引鍵資料表的主索引鍵資料行。|  
|[getDatabaseMajorVersion](../../../connect/jdbc/reference/getdatabasemajorversion-method-sqlserverdatabasemetadata.md)|擷取基礎資料庫的主要版本號碼。|  
|[getDatabaseMinorVersion](../../../connect/jdbc/reference/getdatabaseminorversion-method-sqlserverdatabasemetadata.md)|擷取基礎資料庫的次要版本號碼。|  
|[getDatabaseProductName](../../../connect/jdbc/reference/getdatabaseproductname-method-sqlserverdatabasemetadata.md)|擷取這個資料庫產品的名稱。|  
|[getDatabaseProductVersion](../../../connect/jdbc/reference/getdatabaseproductversion-method-sqlserverdatabasemetadata.md)|擷取這個資料庫產品的版本號碼。|  
|[getDefaultTransactionIsolation](../../../connect/jdbc/reference/getdefaulttransactionisolation-method-sqlserverdatabasemetadata.md)|擷取這個資料庫的預設交易隔離等級。|  
|[getDriverMajorVersion](../../../connect/jdbc/reference/getdrivermajorversion-method-sqlserverdatabasemetadata.md)|擷取這個 JDBC Driver 的主要版本號碼。|  
|[getDriverMinorVersion](../../../connect/jdbc/reference/getdriverminorversion-method-sqlserverdatabasemetadata.md)|擷取這個 JDBC 驅動程式的次要版本號碼。|  
|[getDriverName](../../../connect/jdbc/reference/getdrivername-method-sqlserverdatabasemetadata.md)|擷取這個 JDBC Driver 的名稱。|  
|[getDriverVersion](../../../connect/jdbc/reference/getdriverversion-method-sqlserverdatabasemetadata.md)|擷取這個 JDBC Driver 的版本號碼。|  
|[getExportedKeys](../../../connect/jdbc/reference/getexportedkeys-method-sqlserverdatabasemetadata.md)|擷取外部索引鍵資料行的描述，這些資料行會參考給定資料表的主索引鍵資料行。|  
|[getExtraNameCharacters](../../../connect/jdbc/reference/getextranamecharacters-method-sqlserverdatabasemetadata.md)|擷取可當做未加引號之識別碼名稱的所有額外字元，例如超過 a-z、A-Z、0-9 和 _ 以外的字元。|  
|[getFunctions](../../../connect/jdbc/reference/getfunctions-method-sqlserverdatabasemetadata.md)|擷取系統和使用者函數的描述。|  
|[getFunctionColumns](../../../connect/jdbc/reference/getfunctioncolumns-method-sqlserverdatabasemetadata.md)|擷取所指定目錄的系統函數或使用者函數之參數和傳回類型的描述。|  
|[getIdentifierQuoteString](../../../connect/jdbc/reference/getidentifierquotestring-method-sqlserverdatabasemetadata.md)|擷取**字串**，用來引用 SQL 識別碼。|  
|[getImportedKeys](../../../connect/jdbc/reference/getimportedkeys-method-sqlserverdatabasemetadata.md)|擷取主索引鍵資料行的描述，這些資料行會由資料表的外部索引鍵資料行所參考。|  
|[getIndexInfo](../../../connect/jdbc/reference/getindexinfo-method-sqlserverdatabasemetadata.md)|擷取給定資料表中的索引和統計資料的描述。|  
|[getJDBCMajorVersion](../../../connect/jdbc/reference/getjdbcmajorversion-method-sqlserverdatabasemetadata.md)|擷取這個驅動程式的主要 JDBC 版本號碼。|  
|[getJDBCMinorVersion](../../../connect/jdbc/reference/getjdbcminorversion-method-sqlserverdatabasemetadata.md)|擷取這個驅動程式的次要 JDBC 版本號碼。|  
|[getMaxBinaryLiteralLength](../../../connect/jdbc/reference/getmaxbinaryliterallength-method-sqlserverdatabasemetadata.md)|擷取這個資料庫允許在內嵌二進位常值中使用的最大十六進位字元數目。|  
|[getMaxCatalogNameLength](../../../connect/jdbc/reference/getmaxcatalognamelength-method-sqlserverdatabasemetadata.md)|擷取這個資料庫允許在目錄名稱中使用的最大字元數目。|  
|[getMaxCharLiteralLength](../../../connect/jdbc/reference/getmaxcharliterallength-method-sqlserverdatabasemetadata.md)|擷取這個資料庫允許用於字元常值的最大字元數目。|  
|[getMaxColumnNameLength](../../../connect/jdbc/reference/getmaxcolumnnamelength-method-sqlserverdatabasemetadata.md)|擷取這個資料庫允許用於資料行名稱中的最大字元數目。|  
|[getMaxColumnsInGroupBy](../../../connect/jdbc/reference/getmaxcolumnsingroupby-method-sqlserverdatabasemetadata.md)|擷取這個資料庫允許在 GROUP BY 子句中使用的最大資料行數目。|  
|[getMaxColumnsInIndex](../../../connect/jdbc/reference/getmaxcolumnsinindex-method-sqlserverdatabasemetadata.md)|擷取這個資料庫允許在索引中使用的最大資料行數目。|  
|[getMaxColumnsInOrderBy](../../../connect/jdbc/reference/getmaxcolumnsinorderby-method-sqlserverdatabasemetadata.md)|擷取這個資料庫允許在 ORDER BY 子句中使用的最大資料行數目。|  
|[getMaxColumnsInSelect](../../../connect/jdbc/reference/getmaxcolumnsinselect-method-sqlserverdatabasemetadata.md)|擷取這個資料庫允許在 SELECT 清單中使用的最大資料行數目。|  
|[getMaxColumnsInTable](../../../connect/jdbc/reference/getmaxcolumnsintable-method-sqlserverdatabasemetadata.md)|擷取這個資料庫允許在資料表中使用的最大資料行數目。|  
|[getMaxConnections](../../../connect/jdbc/reference/getmaxconnections-method-sqlserverdatabasemetadata.md)|擷取這個資料庫可能建立的最大並行連接數目。|  
|[getMaxCursorNameLength](../../../connect/jdbc/reference/getmaxcursornamelength-method-sqlserverdatabasemetadata.md)|擷取這個資料庫允許在資料指標名稱中使用的最大字元數目。|  
|[getMaxIndexLength](../../../connect/jdbc/reference/getmaxindexlength-method-sqlserverdatabasemetadata.md)|擷取這個資料庫允許用於索引 (包括索引的各個部分) 的最大位元組數目。|  
|[getMaxProcedureNameLength](../../../connect/jdbc/reference/getmaxprocedurenamelength-method-sqlserverdatabasemetadata.md)|擷取這個資料庫允許在程序名稱中使用的最大字元數目。|  
|[值指出 getMaxRowSize](../../../connect/jdbc/reference/getmaxrowsize-method-sqlserverdatabasemetadata.md)|擷取這個資料庫允許在單一資料列中使用的最大位元組數目。|  
|[getMaxSchemaNameLength](../../../connect/jdbc/reference/getmaxschemanamelength-method-sqlserverdatabasemetadata.md)|擷取這個資料庫允許在結構描述名稱中使用的最大字元數目。|  
|[getMaxStatementLength](../../../connect/jdbc/reference/getmaxstatementlength-method-sqlserverdatabasemetadata.md)|擷取這個資料庫允許在 SQL 陳述式中使用的最大字元數目。|  
|[getMaxStatements](../../../connect/jdbc/reference/getmaxstatements-method-sqlserverdatabasemetadata.md)|擷取這個資料庫可同時開啟的最大作用中陳述式數目。|  
|[getMaxTableNameLength](../../../connect/jdbc/reference/getmaxtablenamelength-method-sqlserverdatabasemetadata.md)|擷取這個資料庫允許在資料表名稱中使用的最大字元數目。|  
|[getMaxTablesInSelect](../../../connect/jdbc/reference/getmaxtablesinselect-method-sqlserverdatabasemetadata.md)|擷取這個資料庫允許在 SELECT 陳述式中使用的最大資料表數目。|  
|[getMaxUserNameLength](../../../connect/jdbc/reference/getmaxusernamelength-method-sqlserverdatabasemetadata.md)|擷取這個資料庫允許在使用者名稱中使用的最大字元數目。|  
|[getNumericFunctions](../../../connect/jdbc/reference/getnumericfunctions-method-sqlserverdatabasemetadata.md)|擷取這個資料庫可用之數學函數的逗號分隔清單。|  
|[getPrimaryKeys](../../../connect/jdbc/reference/getprimarykeys-method-sqlserverdatabasemetadata.md)|擷取給定資料表中的主索引鍵資料行的描述。|  
|[getProcedureColumns](../../../connect/jdbc/reference/getprocedurecolumns-method-sqlserverdatabasemetadata.md)|擷取預存程序參數和結果資料行的描述。|  
|[getProcedures](../../../connect/jdbc/reference/getprocedures-method-sqlserverdatabasemetadata.md)|擷取可依給定目錄、結構描述或預存程序名稱模式取得之預存程序的描述。|  
|[getProcedureTerm](../../../connect/jdbc/reference/getprocedureterm-method-sqlserverdatabasemetadata.md)|擷取慣用詞彙做為這個資料庫中的「程序」。|  
|[getResultSetHoldability](../../../connect/jdbc/reference/getresultsetholdability-method-sqlserverdatabasemetadata.md)|擷取這個資料庫預設結果集保留性。|  
|[getRowIdLifetime](../../../connect/jdbc/reference/getrowidlifetime-method-sqlserverdatabasemetadata.md)|傳回狀態，此狀態會指出是否支援 SQL RowId 資料類型。 如果支援，將傳回 RowId 物件維持有效的存留期間。|  
|[getSchemas](../../../connect/jdbc/reference/getschemas-method.md)|擷取目前資料庫中所提供的結構描述名稱。|  
|[getSchemaTerm](../../../connect/jdbc/reference/getschematerm-method-sqlserverdatabasemetadata.md)|擷取慣用詞彙做為這個資料庫中的「目錄」。|  
|[getSearchStringEscape](../../../connect/jdbc/reference/getsearchstringescape-method-sqlserverdatabasemetadata.md)|擷取**字串**可用來逸出萬用字元。|  
|[getSQLKeywords](../../../connect/jdbc/reference/getsqlkeywords-method-sqlserverdatabasemetadata.md)|擷取這個資料庫的非同時為 SQL92 關鍵字的其他所有 SQL 關鍵字的逗號分隔清單。|  
|[getSQLStateType](../../../connect/jdbc/reference/getsqlstatetype-method-sqlserverdatabasemetadata.md)|指出由 SQLException.getSQLState 方法傳回的 SQLSTATE 是 X/Open (現在稱為 Open Group)、SQL CLI、SQL99 (JDBC 3.0) 或 SQL:2003 (JDBC 4.0)。|  
|[getStringFunctions](../../../connect/jdbc/reference/getstringfunctions-method-sqlserverdatabasemetadata.md)|擷取的逗號分隔清單**字串**函式，可與這個資料庫。|  
|[getSuperTables](../../../connect/jdbc/reference/getsupertables-method-sqlserverdatabasemetadata.md)|擷取資料表階層的描述，這些階層會定義在這個資料庫內的特定結構描述中。|  
|[getSuperTypes](../../../connect/jdbc/reference/getsupertypes-method-sqlserverdatabasemetadata.md)|擷取使用者定義類型階層的描述，這些階層會定義在這個資料庫內的特定結構描述中。|  
|[getSystemFunctions](../../../connect/jdbc/reference/getsystemfunctions-method-sqlserverdatabasemetadata.md)|擷取這個資料庫可用之系統函式的逗號分隔清單。|  
|[getTablePrivileges](../../../connect/jdbc/reference/gettableprivileges-method-sqlserverdatabasemetadata.md)|擷取各個資料表之存取權限的描述，這些資料表會透過給定的目錄、結構描述或資料表名稱模式提供。|  
|[getTables](../../../connect/jdbc/reference/gettables-method-sqlserverdatabasemetadata.md)|擷取可依給定目錄、結構描述或資料表名稱模式取得之資料表的描述。|  
|[getTableTypes](../../../connect/jdbc/reference/gettabletypes-method-sqlserverdatabasemetadata.md)|擷取目前資料庫中所提供的資料表類型。|  
|[getTimeDateFunctions](../../../connect/jdbc/reference/gettimedatefunctions-method-sqlserverdatabasemetadata.md)|擷取這個資料庫可用之時間和日期函數的逗號分隔清單。|  
|[getTypeInfo](../../../connect/jdbc/reference/gettypeinfo-method-sqlserverdatabasemetadata.md)|擷取目前資料庫支援之所有標準 SQL 類型的描述。|  
|[getUDTs](../../../connect/jdbc/reference/getudts-method-sqlserverdatabasemetadata.md)|擷取使用者定義類型的描述，這些類型會定義在特定的結構描述中。|  
|[getURL](../../../connect/jdbc/reference/geturl-method-sqlserverdatabasemetadata.md)|擷取這個資料庫的 URL。|  
|[getUserName](../../../connect/jdbc/reference/getusername-method-sqlserverdatabasemetadata.md)|擷取這個資料庫的已知使用者名稱。|  
|[getVersionColumns](../../../connect/jdbc/reference/getversioncolumns-method-sqlserverdatabasemetadata.md)|擷取資料表的資料行描述，此資料表會在資料列中的任何值更新時自動跟著更新。|  
|[insertsAreDetected](../../../connect/jdbc/reference/insertsaredetected-method-sqlserverdatabasemetadata.md)|擷取是否可以呼叫方法來偵測可見資料列插入[rowInserted](../../../connect/jdbc/reference/rowinserted-method-sqlserverresultset.md)方法[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)類別。|  
|[isCatalogAtStart](../../../connect/jdbc/reference/iscatalogatstart-method-sqlserverdatabasemetadata.md)|擷取值，此值指出目錄是否會出現在完整資料表名稱的開頭。|  
|[isReadOnly](../../../connect/jdbc/reference/isreadonly-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否處在唯讀模式。|  
|[locatorsUpdateCopy](../../../connect/jdbc/reference/locatorsupdatecopy-method-sqlserverdatabasemetadata.md)|指出對 LOB 進行的更新作業是作用於複本或是直接作用於 LOB。|  
|[nullPlusNonNullIsNull](../../../connect/jdbc/reference/nullplusnonnullisnull-method-sqlserverdatabasemetadata.md)|指出這個資料庫是否支援在 NULL 和非 NULL 值之間的串連為 NULL。|  
|[nullsAreSortedAtEnd](../../../connect/jdbc/reference/nullsaresortedatend-method-sqlserverdatabasemetadata.md)|擷取值，此值指出是否一定將 NULL 值排在結尾，無論其排序順序為何。|  
|[nullsAreSortedAtStart](../../../connect/jdbc/reference/nullsaresortedatstart-method-sqlserverdatabasemetadata.md)|擷取值，此值指出是否一定將 NULL 值排在開頭，無論其排序順序為何。|  
|[nullsAreSortedHigh](../../../connect/jdbc/reference/nullsaresortedhigh-method-sqlserverdatabasemetadata.md)|擷取值，此值指出是否將 NULL 值排在最前面。|  
|[nullsAreSortedLow](../../../connect/jdbc/reference/nullsaresortedlow-method-sqlserverdatabasemetadata.md)|擷取值，此值指出是否將 NULL 值排在最後面。|  
|[othersDeletesAreVisible](../../../connect/jdbc/reference/othersdeletesarevisible-method-sqlserverdatabasemetadata.md)|擷取值，此值指出是否可看見其他人所做的刪除。|  
|[othersInsertsAreVisible](../../../connect/jdbc/reference/othersinsertsarevisible-method-sqlserverdatabasemetadata.md)|擷取值，此值指出是否可看見其他人所做的插入。|  
|[othersUpdatesAreVisible](../../../connect/jdbc/reference/othersupdatesarevisible-method-sqlserverdatabasemetadata.md)|擷取值，此值指出是否可看見其他人所完成的更新。|  
|[ownDeletesAreVisible](../../../connect/jdbc/reference/owndeletesarevisible-method-sqlserverdatabasemetadata.md)|擷取值，指出是否可以看見結果集本身的刪除。|  
|[ownInsertsAreVisible](../../../connect/jdbc/reference/owninsertsarevisible-method-sqlserverdatabasemetadata.md)|擷取值，此值指出是否可以看見結果集本身的插入。|  
|[ownUpdatesAreVisible](../../../connect/jdbc/reference/ownupdatesarevisible-method-sqlserverdatabasemetadata.md)|擷取值，此值指出是否可以看見結果集本身的更新。|  
|[storesLowerCaseIdentifiers](../../../connect/jdbc/reference/storeslowercaseidentifiers-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否會依不區分大小寫的方式來處理未加上引號的混合大小寫字母之 SQL 識別碼，並將它們儲存成小寫字母。|  
|[storesLowerCaseQuotedIdentifiers](../../../connect/jdbc/reference/storeslowercasequotedidentifiers-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否會依不區分大小寫的方式來處理已加上引號的混合大小寫字母之 SQL 識別碼，並將它們儲存成小寫字母。|  
|[storesMixedCaseIdentifiers](../../../connect/jdbc/reference/storesmixedcaseidentifiers-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否會依不區分大小寫的方式來處理未加上引號的混合大小寫字母之 SQL 識別碼，並將它們儲存成混合大小寫字母。|  
|[storesMixedCaseQuotedIdentifiers](../../../connect/jdbc/reference/storesmixedcasequotedidentifiers-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否會依不區分大小寫的方式來處理已加上引號的混合大小寫字母之 SQL 識別碼，並將它們儲存成混合大小寫字母。|  
|[storesUpperCaseIdentifiers](../../../connect/jdbc/reference/storesuppercaseidentifiers-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否會依不區分大小寫的方式來處理未加上引號的混合大小寫字母之 SQL 識別碼，並將它們儲存成大寫字母。|  
|[storesUpperCaseQuotedIdentifiers](../../../connect/jdbc/reference/storesuppercasequotedidentifiers-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否會依不區分大小寫的方式來處理已加上引號的混合大小寫字母之 SQL 識別碼，並將它們儲存成大寫字母。|  
|[supportsAlterTableWithAddColumn](../../../connect/jdbc/reference/supportsaltertablewithaddcolumn-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否支援使用加入資料行的 ALTER TABLE。|  
|[supportsAlterTableWithDropColumn](../../../connect/jdbc/reference/supportsaltertablewithdropcolumn-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否支援使用卸除資料行的 ALTER TABLE。|  
|[supportsANSI92EntryLevelSQL](../../../connect/jdbc/reference/supportsansi92entrylevelsql-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否支援 ANSI92 Entry Level SQL 文法。|  
|[supportsANSI92FullSQL](../../../connect/jdbc/reference/supportsansi92fullsql-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否支援 ANSI92 Full SQL 文法。|  
|[supportsANSI92IntermediateSQL](../../../connect/jdbc/reference/supportsansi92intermediatesql-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否支援 ANSI92 Intermediate SQL 文法。|  
|[supportsBatchUpdates](../../../connect/jdbc/reference/supportsbatchupdates-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否支援批次更新。|  
|[supportsCatalogsInDataManipulation](../../../connect/jdbc/reference/supportscatalogsindatamanipulation-method-sqlserverdatabasemetadata.md)|擷取值，此值指出目錄名稱是否可以用於資料操作陳述式。|  
|[supportsCatalogsInIndexDefinitions](../../../connect/jdbc/reference/supportscatalogsinindexdefinitions-method-sqlserverdatabasemetadata.md)|擷取值，此值指出目錄名稱是否可以用於索引定義陳述式。|  
|[supportsCatalogsInPrivilegeDefinitions](../../../connect/jdbc/reference/supportscatalogsinprivilegedefinitions-method-sqlserverdatabasemetadata.md)|擷取值，此值指出目錄名稱是否可以用於權限定義陳述式。|  
|[supportsCatalogsInProcedureCalls](../../../connect/jdbc/reference/supportscatalogsinprocedurecalls-method-sqlserverdatabasemetadata.md)|擷取值，此值指出目錄名稱是否可以用於程序呼叫陳述式。|  
|[supportsCatalogsInTableDefinitions](../../../connect/jdbc/reference/supportscatalogsintabledefinitions-method-sqlserverdatabasemetadata.md)|擷取值，此值指出目錄名稱是否可以用於資料表定義陳述式。|  
|[supportsColumnAliasing](../../../connect/jdbc/reference/supportscolumnaliasing-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否支援設定資料行別名。|  
|[supportsConvert](../../../connect/jdbc/reference/supportsconvert-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否支援在 SQL 型別之間使用 CONVERT 函數。|  
|[supportsCoreSQLGrammar](../../../connect/jdbc/reference/supportscoresqlgrammar-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否支援 ODBC Core SQL 文法。|  
|[supportsCorrelatedSubqueries](../../../connect/jdbc/reference/supportscorrelatedsubqueries-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否支援相互關聯的子查詢。|  
|[supportsDataDefinitionAndDataManipulationTransactions](../../../connect/jdbc/reference/supportsdatadefinitionanddatamanipulationtransactions-method.md)|擷取值，此值指出這個資料庫是否支援在交易中同時使用資料定義陳述式和資料操作陳述式。|  
|[supportsDataManipulationTransactionsOnly](../../../connect/jdbc/reference/supportsdatamanipulationtransactionsonly-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否僅支援在交易中使用資料操作陳述式。|  
|[supportsDifferentTableCorrelationNames](../../../connect/jdbc/reference/supportsdifferenttablecorrelationnames-method-sqlserverdatabasemetadata.md)|擷取值，此值指出當支援資料表相互關聯名稱時，是否會限制這些名稱要不同於資料表的名稱。|  
|[supportsExpressionsInOrderBy](../../../connect/jdbc/reference/supportsexpressionsinorderby-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否支援 ORDER BY 清單中的運算式。|  
|[supportsExtendedSQLGrammar](../../../connect/jdbc/reference/supportsextendedsqlgrammar-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否支援 ODBC Extended SQL 文法。|  
|[supportsFullOuterJoins](../../../connect/jdbc/reference/supportsfullouterjoins-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否支援完整的巢狀外部聯結。|  
|[supportsGetGeneratedKeys](../../../connect/jdbc/reference/supportsgetgeneratedkeys-method-sqlserverdatabasemetadata.md)|擷取值，此值指出是否可以在執行陳述式之後擷取自動產生的索引鍵。|  
|[supportsGroupBy](../../../connect/jdbc/reference/supportsgroupby-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否支援某種形式的 GROUP BY 子句。|  
|[supportsGroupByBeyondSelect](../../../connect/jdbc/reference/supportsgroupbybeyondselect-method-sqlserverdatabasemetadata.md)|擷取值，此值指出在 SELECT 陳述式中的所有資料行都包含於 GROUP BY 子句內的前提下，這個資料庫是否支援在 GROUP BY 子句中使用未包含在 SELECT 陳述式中的資料行。|  
|[supportsGroupByUnrelated](../../../connect/jdbc/reference/supportsgroupbyunrelated-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否支援在 GROUP BY 子句中使用未出現在 SELECT 陳述式中的資料行。|  
|[supportsIntegrityEnhancementFacility](../../../connect/jdbc/reference/supportsintegrityenhancementfacility-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否支援 SQL Integrity Enhancement Facility。|  
|[supportsLikeEscapeClause](../../../connect/jdbc/reference/supportslikeescapeclause-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否支援指定 LIKE 逸出子句。|  
|[supportsLimitedOuterJoins](../../../connect/jdbc/reference/supportslimitedouterjoins-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否提供有限的外部聯結支援。|  
|[supportsMinimumSQLGrammar](../../../connect/jdbc/reference/supportsminimumsqlgrammar-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否支援 ODBC Minimum SQL 文法。|  
|[supportsMixedCaseIdentifiers](../../../connect/jdbc/reference/supportsmixedcaseidentifiers-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否會依不區分大小寫的方式來處理未加上引號的混合大小寫字母之 SQL 識別碼，並將它們儲存成混合大小寫字母。|  
|[supportsMixedCaseQuotedIdentifiers](../../../connect/jdbc/reference/supportsmixedcasequotedidentifiers-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否會依不區分大小寫的方式來處理已加上引號的混合大小寫字母之 SQL 識別碼，並將它們儲存成混合大小寫字母。|  
|[supportsMultipleOpenResults](../../../connect/jdbc/reference/supportsmultipleopenresults-method-sqlserverdatabasemetadata.md)|擷取值，是否可能有多個[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)從傳回的物件[SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)同時物件。|  
|[supportsMultipleResultSets](../../../connect/jdbc/reference/supportsmultipleresultsets-method-sqlserverdatabasemetadata.md)|擷取這個資料庫是否支援取得多個[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件呼叫一次從[執行](../../../connect/jdbc/reference/execute-method.md)方法[SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)類別。|  
|[supportsMultipleTransactions](../../../connect/jdbc/reference/supportsmultipletransactions-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否允許在不同連接上一次開啟多個交易。|  
|[supportsNamedParameters](../../../connect/jdbc/reference/supportsnamedparameters-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否支援在可呼叫陳述式中使用具名參數。|  
|[supportsNonNullableColumns](../../../connect/jdbc/reference/supportsnonnullablecolumns-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫中的資料行是否可以定義成不可為 Null。|  
|[supportsOpenCursorsAcrossCommit](../../../connect/jdbc/reference/supportsopencursorsacrosscommit-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否支援在所有認可之間維持資料指標為開啟狀態。|  
|[supportsOpenCursorsAcrossRollback](../../../connect/jdbc/reference/supportsopencursorsacrossrollback-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否支援在所有回復之間維持資料指標為開啟狀態。|  
|[supportsOpenStatementsAcrossCommit](../../../connect/jdbc/reference/supportsopenstatementsacrosscommit-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否支援在所有認可之間維持陳述式為開啟狀態。|  
|[supportsOpenStatementsAcrossRollback](../../../connect/jdbc/reference/supportsopenstatementsacrossrollback-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否支援在所有回復之間維持陳述式為開啟狀態。|  
|[supportsOrderByUnrelated](../../../connect/jdbc/reference/supportsorderbyunrelated-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否支援在 ORDER BY 子句中使用未出現在 SELECT 陳述式中的資料行。|  
|[supportsOuterJoins](../../../connect/jdbc/reference/supportsouterjoins-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否支援某種形式的外部聯結。|  
|[supportsPositionedDelete](../../../connect/jdbc/reference/supportspositioneddelete-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否支援定位的 DELETE 陳述式。|  
|[supportsPositionedUpdate](../../../connect/jdbc/reference/supportspositionedupdate-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否支援定位的 UPDATE 陳述式。|  
|[supportsResultSetConcurrency](../../../connect/jdbc/reference/supportsresultsetconcurrency-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否支援結合使用給定的並行類型與給定的結果集類型。|  
|[supportsResultSetHoldability](../../../connect/jdbc/reference/supportsresultsetholdability-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否支援給定的結果集保留性。|  
|[supportsResultSetType](../../../connect/jdbc/reference/supportsresultsettype-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否支援給定的結果集類型。|  
|[supportsSavepoints](../../../connect/jdbc/reference/supportssavepoints-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否支援儲存點。|  
|[supportsSchemasInDataManipulation](../../../connect/jdbc/reference/supportsschemasindatamanipulation-method-sqlserverdatabasemetadata.md)|擷取值，此值指出結構描述名稱是否可以用於資料操作陳述式。|  
|[supportsSchemasInIndexDefinitions](../../../connect/jdbc/reference/supportsschemasinindexdefinitions-method-sqlserverdatabasemetadata.md)|擷取值，此值指出結構描述名稱是否可以用於索引定義陳述式。|  
|[supportsSchemasInPrivilegeDefinitions](../../../connect/jdbc/reference/supportsschemasinprivilegedefinitions-method-sqlserverdatabasemetadata.md)|擷取值，此值指出結構描述名稱是否可以用於權限定義陳述式。|  
|[supportsSchemasInProcedureCalls](../../../connect/jdbc/reference/supportsschemasinprocedurecalls-method-sqlserverdatabasemetadata.md)|擷取值，此值指出結構描述名稱是否可以用於程序呼叫陳述式。|  
|[supportsSchemasInTableDefinitions](../../../connect/jdbc/reference/supportsschemasintabledefinitions-method-sqlserverdatabasemetadata.md)|擷取值，此值指出結構描述名稱是否可以用於資料表定義陳述式。|  
|[supportsSelectForUpdate](../../../connect/jdbc/reference/supportsselectforupdate-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否支援 SELECT FOR UPDATE 陳述式。|  
|[supportsStatementPooling](../../../connect/jdbc/reference/supportsstatementpooling-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否支援陳述式共用。|  
|[supportsStoredFunctionsUsingCallSyntax](../../../connect/jdbc/reference/supportsstoredfunctionsusingcallsyntax-method-sqlserverdatabasemetadata.md)|指出目前資料庫是否支援使用預存程序逸出語法來叫用使用者定義函數或供應商定義函數。|  
|[supportsStoredProcedures](../../../connect/jdbc/reference/supportsstoredprocedures-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否支援使用預存程序逸出語法的預存程序呼叫。|  
|[supportsSubqueriesInComparisons](../../../connect/jdbc/reference/supportssubqueriesincomparisons-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否支援在比較運算式中使用子查詢。|  
|[supportsSubqueriesInExists](../../../connect/jdbc/reference/supportssubqueriesinexists-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否支援在 EXISTS 運算式中使用子查詢。|  
|[supportsSubqueriesInIns](../../../connect/jdbc/reference/supportssubqueriesinins-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否支援在 IN 陳述式中使用子查詢。|  
|[supportsSubqueriesInQuantifieds](../../../connect/jdbc/reference/supportssubqueriesinquantifieds-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否支援在定量運算式中使用子查詢。|  
|[supportsTableCorrelationNames](../../../connect/jdbc/reference/supportstablecorrelationnames-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否支援資料表相互關聯名稱。|  
|[supportsTransactionIsolationLevel](../../../connect/jdbc/reference/supportstransactionisolationlevel-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否支援給定的交易隔離等級。|  
|[supportsTransactions](../../../connect/jdbc/reference/supportstransactions-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否支援交易。|  
|[supportsUnion](../../../connect/jdbc/reference/supportsunion-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否支援 SQL UNION。|  
|[supportsUnionAll](../../../connect/jdbc/reference/supportsunionall-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否支援 SQL UNION ALL。|  
|[updatesAreDetected](../../../connect/jdbc/reference/updatesaredetected-method-sqlserverdatabasemetadata.md)|是否可以呼叫來偵測可見資料列更新擷取[rowUpdated](../../../connect/jdbc/reference/rowupdated-method-sqlserverresultset.md)方法[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)類別。|  
|[usesLocalFilePerTable](../../../connect/jdbc/reference/useslocalfilepertable-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否針對每個資料表個別使用檔案。|  
|[usesLocalFiles](../../../connect/jdbc/reference/useslocalfiles-method-sqlserverdatabasemetadata.md)|擷取值，此值指出這個資料庫是否將資料表儲存在本機檔案中。|  
  
## <a name="inherited-methods"></a>繼承的方法  
  
|類別繼承自：|方法|  
|---------------------------|-------------|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Wrapper|isWrapperFor, unwrap|  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
