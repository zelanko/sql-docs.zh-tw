---
title: "sqlsrv_field_metadata |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- sqlsrv_field_metadata
apitype: NA
helpviewer_keywords:
- API Reference, sqlsrv_field_metadata
- sqlsrv_field_metadata
ms.assetid: c02f6942-0484-4567-a78e-fe8aa2053536
caps.latest.revision: 34
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7f7591043014153eb27863b12849aea4e4166639
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsrvfieldmetadata"></a>sqlsrv_field_metadata
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

擷取已備妥陳述式的欄位中繼資料。 如需有關準備陳述式的詳細資訊，請參閱 [sqlsrv_query](../../connect/php/sqlsrv-query.md) 或 [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)。 請注意， **sqlsrv_field_metadata**可以在任何已備妥的陳述式前, 或執行後呼叫。  
  
## <a name="syntax"></a>語法  
  
```  
  
sqlsrv_field_metadata( resource $stmt)  
```  
  
#### <a name="parameters"></a>參數  
*$stmt*：為其尋找欄位中繼資料的陳述式資源。  
  
## <a name="return-value"></a>傳回值  
陣列的 **array** ，或為 **false**。 此陣列包含結果集內各欄位的一個陣列。 每個子陣列都有如下表中所述的索引鍵。 如果擷取欄位中繼資料發生錯誤，則會傳回 **false** 。  
  
|索引鍵|說明|  
|-------|---------------|  
|名稱|欄位所對應的資料行名稱。|  
|型別|對應至 SQL 類型的數值。|  
|大小|字元類型 (char(n)、varchar(n)、nchar(n)、nvarchar(n)、XML) 之欄位的字元數目。 二進位類型 (binary(n)、varbinary(n)、UDT) 之欄位的位元組數目。 **NULL** 適用於其他 SQL Server 資料類型。|  
|有效位數|變數有效位數 (real、numeric、decimal、datetime2、datetimeoffset 和 time) 之類型的有效位數。 **NULL** 適用於其他 SQL Server 資料類型。|  
|小數位數|變數小數位數 (numeric、decimal、datetime2、datetimeoffset 和 time) 之類型的小數位數。 **NULL** 適用於其他 SQL Server 資料類型。|  
|可為 Null|列舉的值，指出資料行是否可為 null (**SQLSRV_NULLABLE_YES**)，資料行不是可為 null (**SQLSRV_NULLABLE_NO**)，或不知道資料行是否可為 null (**SQLSRV_NULLABLE_UNKNOWN**)。|  
  
下表提供有關每個子陣列的索引鍵的詳細資訊 (如需這些類型的詳細資訊，請參閱 SQL Server 文件)：  
  
|SQL Server 2008 資料類型|類型|最小/最大的有效位數|最小/最大的小數位數|大小|  
|-----------------------------|--------|----------------------|------------------|--------|  
|bigint|SQL_BIGINT (-5)|||8|  
|binary|SQL_BINARY (-2)|||0 < *n* < 8000 <sup>1</sup>|  
|bit|SQL_BIT (-7)||||  
|char|SQL_CHAR (1)|||0 < *n* < 8000 <sup>1</sup>|  
|date|SQL_TYPE_DATE (91)|10/10|0/0||  
|datetime|SQL_TYPE_TIMESTAMP (93)|23/23|3/3||  
|datetime2|SQL_TYPE_TIMESTAMP (93)|19/27|0/7||  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET (-155)|26/34|0/7||  
|decimal|SQL_DECIMAL (3)|1/38|0/有效位數值||  
|float|SQL_FLOAT (6)|4/8|||  
|image|SQL_LONGVARBINARY (-4)|||2 GB|  
|int|SQL_INTEGER (4)||||  
|money|SQL_DECIMAL (3)|19/19|4/4||  
|nchar|SQL_WCHAR (-8)|||0 < *n* < 4000 <sup>1</sup>|  
|ntext|SQL_WLONGVARCHAR (-10)|||1 GB|  
|numeric|SQL_NUMERIC (2)|1/38|0/有效位數值||  
|nvarchar|SQL_WVARCHAR (-9)|||0 < *n* < 4000 <sup>1</sup>|  
|real|SQL_REAL (7)|4/4|||  
|smalldatetime|SQL_TYPE_TIMESTAMP (93)|16/16|0/0||  
|smallint|SQL_SMALLINT (5)|||2 個位元組|  
|Smallmoney|SQL_DECIMAL (3)|10/10|4/4||  
|text|SQL_LONGVARCHAR (-1)|||2 GB|  
|time|SQL_SS_TIME2 (-154)|8/16|0/7||  
|timestamp|SQL_BINARY (-2)|||8 個位元組|  
|tinyint|SQL_TINYINT (-6)|||1 個位元組|  
|udt|SQL_SS_UDT (-151)|||變數|  
|uniqueidentifier|SQL_GUID (-11)|||16|  
|varbinary|SQL_VARBINARY (-3)|||0 < *n* < 8000 <sup>1</sup>|  
|varchar|SQL_VARCHAR (12)|||0 < *n* < 8000 <sup>1</sup>|  
|xml|SQL_SS_XML (-152)|||0|  
  
(1) 零 (0) 表示允許大小上限。  
  
可為 Null 的索引鍵可為是或否。  
  
## <a name="example"></a>範例  
下列範例會建立陳述式資源，然後擷取並顯示欄位中繼資料。 此範例假設本機電腦上已安裝 SQL Server 和 [AdventureWorks](http://go.microsoft.com/fwlink/?LinkID=67739) 資料庫。 從命令列執行範例時，所有輸出都會寫入至主控台。  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Prepare the statement. */  
$tsql = "SELECT ReviewerName, Comments FROM Production.ProductReview";  
$stmt = sqlsrv_prepare( $conn, $tsql);  
  
/* Get and display field metadata. */  
foreach( sqlsrv_field_metadata( $stmt) as $fieldMetadata)  
{  
      foreach( $fieldMetadata as $name => $value)  
      {  
           echo "$name: $value\n";  
      }  
      echo "\n";  
}  
  
/* Note: sqlsrv_field_metadata can be called on any statement  
resource, pre- or post-execution. */  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>另請參閱  
[SQLSRV 驅動程式 API 參考](../../connect/php/sqlsrv-driver-api-reference.md)  
[常數 &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  
[關於文件中的程式碼範例](../../connect/php/about-code-examples-in-the-documentation.md)  
  

