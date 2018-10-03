---
title: 常數 (Microsoft Drivers for PHP for SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- constants
ms.assetid: 9727c944-b645-48d6-9012-18dbde35ee3c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 28e5394d824a5999aec90cffb21e07e72dea1691
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47605506"
---
# <a name="constants-microsoft-drivers-for-php-for-sql-server"></a>常數 (Microsoft Drivers for PHP for SQL Server)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本主題討論 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]所定義的常數。  
  
## <a name="pdosqlsrv-driver-constants"></a>PDO_SQLSRV 驅動程式常數  
[PDO 網站](http://php.net/manual/book.pdo.php)上列出的常數在 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 中是有效的。  
  
以下描述 PDO_SQLSRV 驅動程式中的 Microsoft 特定常數。  
  
### <a name="transaction-isolation-level-constants"></a>交易隔離等級常數  
**TransactionIsolation** 索引鍵，可與 [PDO::__construct](../../connect/php/pdo-construct.md)搭配使用，並接受下列其中一個常數：  
  
-   PDO::SQLSRV_TXN_READ_UNCOMMITTED  
  
-   PDO::SQLSRV_TXN_READ_COMMITTED  
  
-   PDO::SQLSRV_TXN_REPEATABLE_READ  
  
-   PDO::SQLSRV_TXN_SNAPSHOT  
  
-   PDO::SQLSRV_TXN_SERIALIZABLE  
  
如需 **TransactionIsolation** 索引鍵的詳細資訊，請參閱 [Connection Options](../../connect/php/connection-options.md)。  
  
### <a name="encoding-constants"></a>編碼常數  
PDO::SQLSRV_ATTR_ENCODING 屬性可以傳遞至 [PDOStatement::setAttribute](../../connect/php/pdostatement-setattribute.md)、[PDO::setAttribute](../../connect/php/pdo-setattribute.md)、[PDO::prepare](../../connect/php/pdo-prepare.md)、[PDOStatement::bindColumn](../../connect/php/pdostatement-bindcolumn.md) 和 [PDOStatement::bindParam](../../connect/php/pdostatement-bindparam.md)。  
  
可傳遞至 PDO::SQLSRV_ATTR_ENCODING 的值為  
  
|PDO_SQLSRV 驅動程式常數|Description|  
|-------------------------------|---------------|  
|PDO::SQLSRV_ENCODING_BINARY|資料是來自伺服器的原始位元組資料流，未執行編碼或轉譯。<br /><br />對 PDO::setAttribute 而言無效。|  
|PDO::SQLSRV_ENCODING_SYSTEM|資料是 8 位元字元，如同在系統上設定之 Windows 地區設定的字碼頁所指定。 系統會以單一位元組問號 (?) 字元取代任何多位元組字元或未對應到此字碼頁的字元。|  
|PDO::SQLSRV_ENCODING_UTF8|資料採用 UTF-8 編碼。 這是預設編碼。|  
|PDO::SQLSRV_ENCODING_DEFAULT|如果在連接期間指定，則使用 PDO::SQLSRV_ENCODING_SYSTEM。<br /><br />如果是在準備陳述式中指定的，則使用連接的編碼。|  
  
### <a name="query-timeout"></a>查詢逾時  
PDO::SQLSRV_ATTR_QUERY_TIMEOUT 屬性是任何代表逾時期間 (秒) 的非負數整數。 零 (0) 預設值，表示沒有逾時。  
  
您可以使用 [PDOStatement::setAttribute](../../connect/php/pdostatement-setattribute.md)、[PDO::setAttribute](../../connect/php/pdo-setattribute.md) 和 [PDO::prepare](../../connect/php/pdo-prepare.md) 來指定 PDO::SQLSRV_ATTR_QUERY_TIMEOUT 屬性。  
  
### <a name="direct-or-prepared-execution"></a>直接或備妥的執行  
您可以使用 PDO::SQLSRV_ATTR_DIRECT_QUERY 屬性，選取直接查詢執行或備妥的陳述式執行。 PDO::SQLSRV_ATTR_DIRECT_QUERY 可以用 [PDO::prepare](../../connect/php/pdo-prepare.md) 或 [PDO::setAttribute](../../connect/php/pdo-setattribute.md) 來設定。 如需 PDO::SQLSRV_ATTR_DIRECT_QUERY 的詳細資訊，請參閱 [PDO_SQLSRV 驅動程式中的直接陳述式執行和已備妥的陳述式執行](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md)。  

### <a name="handling-numeric-fetches"></a>處理數值擷取
PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE 屬性可用來處理從資料行的數值提取和數值 SQL 型別 （位元、 整數、 smallint、 tinyint、 float 和 real）。 PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE 當設定為 true 時，整數資料行的結果會會表示為 int，而 SQL 浮點數和 reals 會表示為浮點數。 這個屬性可以設定具有[pdostatement:: Setattribute](../../connect/php/pdostatement-setattribute.md)。 


## <a name="sqlsrv-driver-constants"></a>SQLSRV 驅動程式常數  
下列各節列出 SQLSRV 驅動程式所使用的常數。  
  
### <a name="err-constants"></a>ERR 常數  
下表列出用來指定 [sqlsrv_errors](../../connect/php/sqlsrv-errors.md) 會傳回錯誤、警告還是兩者都傳回的常數。  
  
|ReplTest1|Description|  
|---------|---------------|  
|SQLSRV_ERR_ALL|傳回上次呼叫 **sqlsrv** 函數時產生的錯誤和警告。 這是預設值。|  
|SQLSRV_ERR_ERRORS|傳回上次呼叫 **sqlsrv** 函數時產生的錯誤。|  
|SQLSRV_ERR_WARNINGS|傳回上次呼叫 **sqlsrv** 函數時產生的警告。|  
  
### <a name="fetch-constants"></a>FETCH 常數  
下表列出用來指定 [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md)所傳回之陣列類型的常數。  
  
|SQLSRV 常數|Description|  
|-------------------|---------------|  
|SQLSRV_FETCH_ASSOC|**sqlsrv_fetch_array** 會以關聯陣列的形式傳回下一個資料列。|  
|SQLSRV_FETCH_BOTH|**sqlsrv_fetch_array** 會以同時具有數值和關聯索引鍵的陣列形式傳回下一個資料列。 這是預設值。|  
|SQLSRV_FETCH_NUMERIC|**sqlsrv_fetch_array** 會以數值索引陣列的形式傳回下一個資料列。|  
  
### <a name="logging-constants"></a>記錄常數  
此節列出用來透過 [sqlsrv_configure](../../connect/php/sqlsrv-configure.md)變更記錄設定的常數。 如需記錄活動的詳細資訊，請參閱 [Logging Activity](../../connect/php/logging-activity.md)。  
  
下表列出可做為 **LogSubsystems** 設定值的常數：  
  
|SQLSRV 常數 (括弧中的整數對等項目)|Description|  
|----------------------------------------------------------|---------------|  
|SQLSRV_LOG_SYSTEM_ALL (-1)|開啟所有子系統的記錄。|  
|SQLSRV_LOG_SYSTEM_CONN (2)|開啟連接活動的記錄。|  
|SQLSRV_LOG_SYSTEM_INIT (1)|開啟初始化活動的記錄。|  
|SQLSRV_LOG_SYSTEM_OFF (0)|關閉記錄。|  
|SQLSRV_LOG_SYSTEM_STMT (4)|開啟陳述式活動的記錄。|  
|SQLSRV_LOG_SYSTEM_UTIL (8)|開啟錯誤函式活動 (例如 **handle_error** 和 **handle_warning**) 的記錄。|  
  
下表列出可做為 **LogSeverity** 設定值的常數：  
  
|SQLSRV 常數 (括弧中的整數對等項目)|Description|  
|----------------------------------------------------------|---------------|  
|SQLSRV_LOG_SEVERITY_ALL (-1)|指定將會記錄錯誤、警告和通知。|  
|SQLSRV_LOG_SEVERITY_ERROR (1)|指定將會記錄錯誤。|  
|SQLSRV_LOG_SEVERITY_NOTICE (4)|指定將會記錄通知。|  
|SQLSRV_LOG_SEVERITY_WARNING (2)|指定將會記錄警告。|  
  
### <a name="nullable-constants"></a>Nullable 常數  
下表列出可用來判斷資料行是否可為 Null 或這項資訊是否無法使用的常數。 您可以比較 **sqlsrv_field_metadata** 所傳回的 [Nullable](../../connect/php/sqlsrv-field-metadata.md) 索引鍵值，以判斷資料行可為 Null 的狀態。  
  
|SQLSRV 常數 (括弧中的整數對等項目)|Description|  
|----------------------------------------------------------|---------------|  
|SQLSRV_NULLABLE_YES (0)|此資料行可為 null。|  
|SQLSRV_NULLABLE_NO (1)|資料行不可為 Null。|  
|SQLSRV_NULLABLE_UNKNOWN (2)|不知道資料行是否可為 Null。|  
  
### <a name="param-constants"></a>PARAM 常數  
下列清單包含在您呼叫 [sqlsrv_query](../../connect/php/sqlsrv-query.md) 或 [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)時用來指定參數方向的常數。  
  
|SQLSRV 常數|Description|  
|-------------------|---------------|  
|SQLSRV_PARAM_IN|表示輸入參數。|  
|SQLSRV_PARAM_INOUT|表示雙向參數。|  
|SQLSRV_PARAM_OUT|表示輸出參數。|  
  
### <a name="phptype-constants"></a>PHPTYPE 常數  
下表列出用來說明 PHP 資料類型的常數。 如需 PHP 資料類型的資訊，請參閱 [PHP 類型](http://php.net/manual/en/language.types.php)。  
  
|SQLSRV 常數|PHP 資料類型|  
|-------------------|-----------------|  
|SQLSRV_PHPTYPE_INT|Integer|  
|SQLSRV_PHPTYPE_DATETIME|DATETIME|  
|SQLSRV_PHPTYPE_FLOAT|float|  
|SQLSRV_PHPTYPE_STREAM ($編碼<sup>1</sup>)|STREAM|  
|SQLSRV_PHPTYPE_STRING ($編碼<sup>1</sup>)|String|  
  
1. **SQLSRV_PHPTYPE_STREAM** 和 **SQLSRV_PHPTYPE_STRING** 可接受指定資料流編碼的參數。 下表包含是可接受之參數的 SQLSRV 常數，以及對應編碼的描述。  
  
|SQLSRV 常數|Description|  
|-------------------|---------------|  
|SQLSRV_ENC_BINARY|資料會以原始位元組資料流形式從伺服器傳回，而不需執行編碼或轉譯。|  
|SQLSRV_ENC_CHAR|資料會以如同在系統上設定之 Windows 地區設定的字碼頁中指定的 8 位元字元傳回。 系統會以單一位元組問號 (?) 字元取代任何多位元組字元或未對應到此字碼頁的字元。<br /><br />這是預設編碼。|  
|"UTF-8"|資料會以 UTF-8 編碼傳回。 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]1.1 版已加入此常數。 如需 UTF-8 支援的詳細資訊，請參閱[如何：使用內建的 UTF-8 支援傳送及接收 UTF-8 資料](../../connect/php/how-to-send-and-retrieve-utf-8-data-using-built-in-utf-8-support.md)。|  
  
> [!NOTE]  
> 當您使用 **SQLSRV_PHPTYPE_STREAM** 或 **SQLSRV_PHPTYPE_STRING** 時，必須要指定編碼。 如果未提供參數，將會傳回錯誤。  
  
如需這些常數的詳細資訊，請參閱 [如何：指定 PHP 資料類型](../../connect/php/how-to-specify-php-data-types.md)、 [如何：使用 SQLSRV 驅動程式以資料流的形式擷取字元資料](../../connect/php/how-to-retrieve-character-data-as-a-stream-using-the-sqlsrv-driver.md)。  
  
### <a name="sqltype-constants"></a>SQLTYPE 常數  
下表列出用來說明 SQL Server 資料類型的常數。 某些常數是類似的函式，而且可能需要對應的參數，有效位數、 小數位數和/或長度。  當繫結參數，則應該使用類似函式的常數。 型別比較，就需要有標準的 （非函式類似） 常數。 如需 SQL Server 資料類型的資訊，請參閱[資料類型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)。 如需有效位數、小數位數和長度的資訊，請參閱[有效位數、小數位數和長度 (Transact-SQL)](../../t-sql/data-types/precision-scale-and-length-transact-sql.md)。  
  
|SQLSRV 常數|SQL Server 資料類型|  
|-------------------|------------------------|  
|SQLSRV_SQLTYPE_BIGINT|BIGINT|  
|SQLSRV_SQLTYPE_BINARY|BINARY|  
|SQLSRV_SQLTYPE_BIT|bit|  
|SQLSRV_SQLTYPE_CHAR|char<sup>5</sup>|  
|SQLSRV_SQLTYPE_CHAR($charCount)|char|  
|SQLSRV_SQLTYPE_DATE|date<sup>4</sup>|  
|SQLSRV_SQLTYPE_DATETIME|DATETIME|  
|SQLSRV_SQLTYPE_DATETIME2|datetime2<sup>4</sup>|  
|SQLSRV_SQLTYPE_DATETIMEOFFSET|datetimeoffset<sup>4</sup>|  
|SQLSRV_SQLTYPE_DECIMAL|十進位<sup>5</sup>|
|SQLSRV_SQLTYPE_DECIMAL($precision, $scale)|Decimal|  
|SQLSRV_SQLTYPE_FLOAT|FLOAT|  
|SQLSRV_SQLTYPE_IMAGE|image<sup>1</sup>|  
|SQLSRV_SQLTYPE_INT|ssNoversion|  
|SQLSRV_SQLTYPE_MONEY|money| 
|SQLSRV_SQLTYPE_NCHAR|nchar<sup>5</sup>|   
|SQLSRV_SQLTYPE_NCHAR($charCount)|NCHAR|  
|SQLSRV_SQLTYPE_NUMERIC|數值<sup>5</sup>|
|SQLSRV_SQLTYPE_NUMERIC($precision, $scale)|NUMERIC|  
|SQLSRV_SQLTYPE_NVARCHAR|nvarchar<sup>5</sup>|  
|SQLSRV_SQLTYPE_NVARCHAR($charCount)|NVARCHAR|  
|SQLSRV_SQLTYPE_NVARCHAR('max')|nvarchar(MAX)|  
|SQLSRV_SQLTYPE_NTEXT|ntext<sup>2</sup>|  
|SQLSRV_SQLTYPE_REAL|REAL|  
|SQLSRV_SQLTYPE_SMALLDATETIME|smalldatetime|  
|SQLSRV_SQLTYPE_SMALLINT|SMALLINT|  
|SQLSRV_SQLTYPE_SMALLMONEY|SMALLMONEY|  
|SQLSRV_SQLTYPE_TEXT|text<sup>3</sup>|  
|SQLSRV_SQLTYPE_TIME|time<sup>4</sup>|  
|SQLSRV_SQLTYPE_TIMESTAMP|TIMESTAMP|  
|SQLSRV_SQLTYPE_TINYINT|TINYINT|  
|SQLSRV_SQLTYPE_UNIQUEIDENTIFIER|UNIQUEIDENTIFIER|  
|SQLSRV_SQLTYPE_UDT|UDT|  
|SQLSRV_SQLTYPE_VARBINARY|varbinary<sup>5</sup>|  
|SQLSRV_SQLTYPE_VARBINARY($byteCount)|varbinary|  
|SQLSRV_SQLTYPE_VARBINARY('max')|varbinary(MAX)|  
|SQLSRV_SQLTYPE_VARCHAR|varchar<sup>5</sup>|  
|SQLSRV_SQLTYPE_VARCHAR($charCount)|varchar|  
|SQLSRV_SQLTYPE_VARCHAR('max')|varchar(MAX)|  
|SQLSRV_SQLTYPE_XML|xml|  
  
1.  這是對應至 varbinary(max) 類型的傳統類型。  
  
2.  這是對應至較新 nvarchar 類型的傳統類型。  
  
3.  這是對應至較新 varchar 類型的傳統類型。  
  
4.  [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]1.1 版已加入此類型的支援。  

5.  這些常數應該用於型別比較作業，並不取代類似的語法類似函式的常數。 繫結參數，您應該使用類似函式的常數。

  
下表列出接受參數的 SQLTYPE 常數，以及允許的參數值範圍。  
  
|SQLTYPE|參數|允許的參數範圍|  
|-----------|-------------|---------------------------------|  
|SQLSRV_SQLTYPE_CHAR、<br /><br />SQLSRV_SQLTYPE_VARCHAR|charCount|1 - 8000|  
|SQLSRV_SQLTYPE_NCHAR、<br /><br />SQLSRV_SQLTYPE_NVARCHAR|charCount|1 - 4000|  
|SQLSRV_SQLTYPE_BINARY、<br /><br />SQLSRV_SQLTYPE_VARBINARY|byteCount|1 - 8000|  
|SQLSRV_SQLTYPE_DECIMAL、<br /><br />SQLSRV_SQLTYPE_NUMERIC|有效位數|1 - 38|  
|SQLSRV_SQLTYPE_DECIMAL、<br /><br />SQLSRV_SQLTYPE_NUMERIC|scale|1 - 有效位數|  
  
### <a name="transaction-isolation-level-constants"></a>交易隔離等級常數  
**TransactionIsolation** 索引鍵，可與 [sqlsrv_connect](../../connect/php/sqlsrv-connect.md)搭配使用，並接受下列其中一個常數：  
  
-   SQLSRV_TXN_READ_UNCOMMITTED  
  
-   SQLSRV_TXN_READ_COMMITTED  
  
-   SQLSRV_TXN_REPEATABLE_READ  
  
-   SQLSRV_TXN_SNAPSHOT  
  
-   SQLSRV_TXN_SERIALIZABLE  
  
### <a name="cursor-and-scrolling-constants"></a>資料指標和捲動常數  
下列常數指定您可以在結果集內使用的資料指標類型：  
  
-   SQLSRV_CURSOR_FORWARD  
  
-   SQLSRV_CURSOR_STATIC  
  
-   SQLSRV_CURSOR_DYNAMIC  
  
-   SQLSRV_CURSOR_KEYSET  
  
-   SQLSRV_CURSOR_CLIENT_BUFFERED  
  
下列常數指定要在結果集內選取的資料列：  
  
-   SQLSRV_SCROLL_NEXT  
  
-   SQLSRV_SCROLL_PRIOR  
  
-   SQLSRV_SCROLL_FIRST  
  
-   SQLSRV_SCROLL_LAST  
  
-   SQLSRV_SCROLL_ABSOLUTE  
  
-   SQLSRV_SCROLL_RELATIVE  
  
如需使用這些常數的相關資訊，請參閱 [Specifying a Cursor Type and Selecting Rows](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md)。  
  
## <a name="see-also"></a>另請參閱  
[SQLSRV 驅動程式 API 參考](../../connect/php/sqlsrv-driver-api-reference.md)  
  
