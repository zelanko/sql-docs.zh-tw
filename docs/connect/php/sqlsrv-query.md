---
title: sqlsrv_query | Microsoft Docs
ms.custom: ''
ms.date: 04/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_query
apitype: NA
helpviewer_keywords:
- sqlsrv_query
- executing queries
- API Reference, sqlsrv_query
ms.assetid: 9fa7c4c8-4da8-4299-9893-f61815055aa3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8ce7a12b3964e3e0c2407521978df03af9d88f63
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "68014967"
---
# <a name="sqlsrv_query"></a>sqlsrv_query
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

準備及執行陳述式。  
  
## <a name="syntax"></a>語法  
  
```  
  
sqlsrv_query(resource $conn, string $tsql [, array $params [, array $options]])  
```  
  
#### <a name="parameters"></a>參數  
*$conn*：與備妥的陳述式相關聯的連接資源。  
  
*$tsql*：與已備妥陳述式相對應的 Transact-SQL 運算式。  
  
*$params* [選用]：與參數化查詢中之參數對應的值**陣列**。 陣列的每個元素可以是下列其中一項：
  
-   常值。  
  
-   PHP 變數。  
  
-   具有下列結構的 **陣列** ：  
  
    ```  
    array($value [, $direction [, $phpType [, $sqlType]]])  
    ```  
  
    下表描述陣列的每個項目：  
  
    |元素|描述|  
    |-----------|---------------|  
    |*$value*|常值、PHP 變數或 PHP by-reference 變數。|  
    |*$direction*[OPTIONAL]|下列其中一項 **SQLSRV_PARAM_\*** 常數，用於指定參數方向：**SQLSRV_PARAM_IN**、**SQLSRV_PARAM_OUT**、**SQLSRV_PARAM_INOUT**。 預設值為 **SQLSRV_PARAM_IN**。<br /><br />如需 PHP 常數的詳細資訊，請參閱 [常數 &#40;適用於 SQL Server 之 PHP 的 Microsoft 驅動程序&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)。|  
    |*$phpType*[OPTIONAL]|**SQLSRV_PHPTYPE_\*** 常數，指定傳回值的 PHP 資料類型。<br /><br />如需 PHP 常數的詳細資訊，請參閱 [常數 &#40;適用於 SQL Server 之 PHP 的 Microsoft 驅動程序&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)。|  
    |*$sqlType*[OPTIONAL]|**SQLSRV_SQLTYPE_\*** 常數，指定輸入值的 SQL Server 資料類型。<br /><br />如需 PHP 常數的詳細資訊，請參閱 [常數 &#40;適用於 SQL Server 之 PHP 的 Microsoft 驅動程序&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)。|  
  
*$options* [選用]：設定查詢屬性的關聯陣列。 它與 [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md#properties) 也支援的索引鍵清單相同。
  
## <a name="return-value"></a>傳回值  
陳述式資源。 如果無法建立且 (或) 無法執行陳述式，將會傳回 **false**。  
  
## <a name="remarks"></a>備註  
**sqlsrv_query** 函式非常適用於一次性查詢，且應作為執行查詢的預設選擇 (除非情況特殊)。 此函數提供簡便的方法，可用最少量的程式碼來執行查詢。 **sqlsrv_query** 函式可執行陳述式準備和陳述式執行，而且可用來執行參數化查詢。  
  
如需詳細資訊，請參閱 [如何：使用 SQLSRV 驅動程式擷取輸出參數](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)。  
  
## <a name="example"></a>範例  
在下列範例中，會將單一資料列插入 AdventureWorks 資料庫的 *Sales.SalesOrderDetail* 資料表中。 此範例假設本機電腦上已安裝 SQL Server 和 [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) 資料庫。 從命令列執行範例時，所有輸出都會寫入至主控台。  
  
> [!NOTE]  
> 雖然下列範例會使用 INSERT 陳述式示範 **sqlsrv_query** 如何用於一次性陳述式執行，但此概念也適用於任何 Transact-SQL 陳述式。  
  
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
下列範例會更新 AdventureWorks 資料庫之 *Sales.SalesOrderDetail* 資料表中的欄位。 此範例假設本機電腦上已安裝 SQL Server 和 [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) 資料庫。 從命令列執行範例時，所有輸出都會寫入至主控台。  
  
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
> 建議在將值繫結至 [decimal 或 numeric 資料行](https://docs.microsoft.com/sql/t-sql/data-types/decimal-and-numeric-transact-sql)時使用字串作為輸入，以確保精確度與正確性，因為 PHP 所具備的[浮點數](https://php.net/manual/en/language.types.float.php) \(英文\) 精確度有限。 這同樣適用於 bigint 資料行，尤其當值不在某個[整數](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)的範圍內時。

## <a name="example"></a>範例  
此程式碼範例示範如何繫結十進位值作為輸入參數。  

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

## <a name="example"></a>範例
此程式碼範例示範如何建立 [sql_variant](https://docs.microsoft.com/sql/t-sql/data-types/sql-variant-transact-sql) 類型的資料表，並擷取插入的資料。

```
<?php
$server = 'serverName';
$dbName = 'databaseName';
$uid = 'yourUserName';
$pwd = 'yourPassword';

$options = array("Database"=>$dbName, "UID"=>$uid, "PWD"=>$pwd);
$conn = sqlsrv_connect($server, $options);
if($conn === false) {
    die(print_r(sqlsrv_errors(), true));
}

$tableName = 'testTable';
$query = "CREATE TABLE $tableName ([c1_int] sql_variant, [c2_varchar] sql_variant)";

$stmt = sqlsrv_query($conn, $query);
if($stmt === false) {
    die(print_r(sqlsrv_errors(), true));
}
sqlsrv_free_stmt($stmt);

$query = "INSERT INTO [$tableName] (c1_int, c2_varchar) VALUES (1, 'test_data')";
$stmt = sqlsrv_query($conn, $query);
if($stmt === false) {
    die(print_r(sqlsrv_errors(), true));
}
sqlsrv_free_stmt($stmt);

$query = "SELECT * FROM $tableName";
$stmt = sqlsrv_query($conn, $query);

if(sqlsrv_fetch($stmt) === false) {
    die(print_r(sqlsrv_errors(), true));
}

$col1 = sqlsrv_get_field($stmt, 0);
echo "First field:  $col1 \n";

$col2 = sqlsrv_get_field($stmt, 1);
echo "Second field:  $col2 \n";

sqlsrv_free_stmt($stmt);
sqlsrv_close($conn);

?>
```

預期的輸出會是：

```
First field:  1
Second field:  test_data
```

## <a name="see-also"></a>另請參閱  
[SQLSRV 驅動程式 API 參考](../../connect/php/sqlsrv-driver-api-reference.md)  

[如何：執行參數化查詢](../../connect/php/how-to-perform-parameterized-queries.md)  

[關於文件中的程式碼範例](../../connect/php/about-code-examples-in-the-documentation.md)  

[如何：以資料流形式傳送資料](../../connect/php/how-to-send-data-as-a-stream.md)  

[使用方向參數](../../connect/php/using-directional-parameters.md)  

  
