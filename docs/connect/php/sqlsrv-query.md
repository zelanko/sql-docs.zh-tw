---
title: sqlsrv_query |Microsoft 文件
ms.custom: ''
ms.date: 05/22/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- sqlsrv_query
apitype: NA
helpviewer_keywords:
- sqlsrv_query
- executing queries
- API Reference, sqlsrv_query
ms.assetid: 9fa7c4c8-4da8-4299-9893-f61815055aa3
caps.latest.revision: 46
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1dd1dac24574484f0424399504f606f6b0917aa8
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35309497"
---
# <a name="sqlsrvquery"></a>sqlsrv_query
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

準備及執行陳述式。  
  
## <a name="syntax"></a>語法  
  
```  
  
sqlsrv_query(resource $conn, string $tsql [, array $params [, array $options]])  
```  
  
#### <a name="parameters"></a>參數  
*$conn*：與備妥的陳述式相關聯的連接資源。  
  
*$tsql*： 對應至已備妥的陳述式的 TRANSACT-SQL 運算式。  
  
*$params* [選用]:**陣列**對應到參數化查詢中的值。 陣列的每個元素可以是下列其中一項：
  
-   常值。  
  
-   PHP 變數。  
  
-   具有下列結構的 **陣列** ：  
  
    ```  
    array($value [, $direction [, $phpType [, $sqlType]]])  
    ```  
  
    下表中，為陣列的每個元素的描述：  
  
    |元素|描述|  
    |-----------|---------------|  
    |*$value*|常值、PHP 變數或 PHP by-reference 變數。|  
    |*$direction*[選擇性]|下列其中一種**SQLSRV_PARAM_\*** 用來指出參數方向的常數： **SQLSRV_PARAM_IN**， **SQLSRV_PARAM_OUT**， **SQLSRV_PARAM_INOUT**。 預設值是**SQLSRV_PARAM_IN**。<br /><br />如需 PHP 常數的詳細資訊，請參閱[常數&#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)。|  
    |*$phpType*[OPTIONAL]|A **SQLSRV_PHPTYPE_\*** 指定 PHP 資料類型傳回值的常數。<br /><br />如需 PHP 常數的詳細資訊，請參閱[常數&#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)。|  
    |*$sqlType*[OPTIONAL]|A **SQLSRV_SQLTYPE_\*** 指定輸入值的 SQL Server 資料類型的常數。<br /><br />如需 PHP 常數的詳細資訊，請參閱[常數&#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)。|  
  
*$options* [選用]: 設定查詢屬性的關聯陣列。 支援的索引鍵如下所示：  
  
|索引鍵|支援的值|描述|  
|-------|--------------------|---------------|  
|QueryTimeout|正整數值。|設定查詢逾時 (以秒為單位)。 根據預設，此驅動程式無限期地等候結果。|  
|SendStreamParamsAtExec|**[True]** 或 **[False]**<br /><br />預設值為 **true**。|設定要傳送所有的資料流資料執行的驅動程式 (**true**)，或以區塊傳送資料流資料 (**false**)。 依預設，此值設定為 **true**。 如需詳細資訊，請參閱 [sqlsrv_send_stream_data](../../connect/php/sqlsrv-send-stream-data.md)。|  
|可捲動|SQLSRV_CURSOR_FORWARD<br /><br />SQLSRV_CURSOR_STATIC<br /><br />SQLSRV_CURSOR_DYNAMIC<br /><br />SQLSRV_CURSOR_KEYSET<br /><br />SQLSRV_CURSOR_CLIENT_BUFFERED|如需這些值的詳細資訊，請參閱 [指定資料指標類型及選取資料列](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md)。|  
  
## <a name="return-value"></a>傳回值  
陳述式資源。 如果陳述式會建立及/或無法執行， **false**傳回。  
  
## <a name="remarks"></a>備註  
**Sqlsrv_query**函式是非常適用於一次性查詢，而且應該是預設選項來執行查詢，除非情況特殊。 此函數提供簡便的方法，可用最少量的程式碼來執行查詢。 **Sqlsrv_query**函數可執行陳述式準備和陳述式執行，而且可用來執行參數化的查詢。  
  
如需詳細資訊，請參閱 [How to: Retrieve Output Parameters Using the SQLSRV Driver](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)。  
  
## <a name="example"></a>範例  
在下列範例中，會將單一資料列插入 AdventureWorks 資料庫的 *Sales.SalesOrderDetail* 資料表中。 此範例假設 SQL Server 和[AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works)資料庫安裝在本機電腦上。 從命令列執行範例時，所有輸出都會寫入至主控台。  
  
> [!NOTE]  
> 雖然下列範例會使用 INSERT 陳述式示範如何使用**sqlsrv_query**用於一次性陳述式執行時，概念也適用於任何 Transact SQL 陳述式。  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array("Database"=>"AdventureWorks");  
$conn = sqlsrv_connect($serverName, $connectionInfo);  
if ($conn === false) {  
    echo "Could not connect.\n";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
/* Set up the parameterized query. */  
$tsql = "INSERT INTO Sales.SalesOrderDetail   
        (SalesOrderID,   
         OrderQty,   
         ProductID,   
         SpecialOfferID,   
         UnitPrice,   
         UnitPriceDiscount)  
        VALUES   
        (?, ?, ?, ?, ?, ?)";  
  
/* Set parameter values. */  
$params = array(75123, 5, 741, 1, 818.70, 0.00);  
  
/* Prepare and execute the query. */  
$stmt = sqlsrv_query($conn, $tsql, $params);  
if ($stmt) {  
    echo "Row successfully inserted.\n";  
} else {  
    echo "Row insertion failed.\n";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt($stmt);  
sqlsrv_close($conn);  
?>  
```  
  
## <a name="example"></a>範例  
下列範例會更新中的欄位*Sales.SalesOrderDetail* AdventureWorks 資料庫的資料表。 此範例假設 SQL Server 和[AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works)資料庫安裝在本機電腦上。 從命令列執行範例時，所有輸出都會寫入至主控台。  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array("Database"=>"AdventureWorks");  
$conn = sqlsrv_connect($serverName, $connectionInfo);  
if ($conn === false) {  
    echo "Could not connect.\n";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
/* Set up the parameterized query. */  
$tsql = "UPDATE Sales.SalesOrderDetail   
         SET OrderQty = (?)   
         WHERE SalesOrderDetailID = (?)";  
  
/* Assign literal parameter values. */  
$params = array(5, 10);  
  
/* Execute the query. */  
if (sqlsrv_query($conn, $tsql, $params)) {  
    echo "Statement executed.\n";  
} else {  
    echo "Error in statement execution.\n";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
/* Free connection resources. */  
sqlsrv_close($conn);  
?>  
```  
  
> [!NOTE]
> 建議使用字串做為輸入，當繫結至值[十進位或數值資料行](https://docs.microsoft.com/en-us/sql/t-sql/data-types/decimal-and-numeric-transact-sql)為確保如 PHP 有限的有效位數的有效位數和精確度[浮點數](http://php.net/manual/en/language.types.float.php)。 同樣適用於 bigint 資料行，尤其是有效值的範圍外[整數](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)。

## <a name="example"></a>範例  
此程式碼範例示範如何將繫結十進位值做為輸入參數。  

```
<?php
$serverName = "(local)";
$connectionInfo = array("Database"=>"YourTestDB");  
$conn = sqlsrv_connect($serverName, $connectionInfo);  
if ($conn === false) {  
     echo "Could not connect.\n";  
     die(print_r(sqlsrv_errors(), true));  
}  

// Assume TestTable exists with a decimal field 
$input = "9223372036854.80000";
$params = array($input);
$stmt = sqlsrv_query($conn, "INSERT INTO TestTable (DecimalCol) VALUES (?)", $params);

sqlsrv_free_stmt($stmt);  
sqlsrv_close($conn);  

?>
```


## <a name="see-also"></a>另請參閱  
[SQLSRV 驅動程式 API 參考](../../connect/php/sqlsrv-driver-api-reference.md)  

[如何：執行參數化查詢](../../connect/php/how-to-perform-parameterized-queries.md)  

[關於文件中的程式碼範例](../../connect/php/about-code-examples-in-the-documentation.md)  

[如何：以資料流形式傳送資料](../../connect/php/how-to-send-data-as-a-stream.md)  

[使用方向參數](../../connect/php/using-directional-parameters.md)  

  
