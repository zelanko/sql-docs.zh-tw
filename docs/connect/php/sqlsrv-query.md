---
title: sqlsrv_query |Microsoft Docs
ms.custom: ''
ms.date: 08/01/2018
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
ms.openlocfilehash: 45a25840023772d835fd2bbfbadf2977bfa90107
ms.sourcegitcommit: ef7f2540ba731cc6a648005f2773d759df5c6405
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/02/2018
ms.locfileid: "39415517"
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
  
*$tsql*：與已備妥陳述式相對應的 Transact-SQL 運算式。  
  
*$params* [選用]：與參數化查詢中之參數對應的值**陣列**。 陣列的每個元素可以是下列其中一項：
  
-   常值。  
  
-   PHP 變數。  
  
-   具有下列結構的 **陣列** ：  
  
    ```  
    array($value [, $direction [, $phpType [, $sqlType]]])  
    ```  
  
    下表描述陣列的每個項目：  
  
    |元素|Description|  
    |-----------|---------------|  
    |*$value*|常值、PHP 變數或 PHP by-reference 變數。|  
    |*$direction*[選用]|下列其中一項 **SQLSRV_PARAM_\*** 常數，用於指定參數方向：**SQLSRV_PARAM_IN**、**SQLSRV_PARAM_OUT**、**SQLSRV_PARAM_INOUT**。 預設值為 **SQLSRV_PARAM_IN**。<br /><br />如需 PHP 常數的詳細資訊，請參閱 [常數 &#40;適用於 SQL Server 之 PHP 的 Microsoft 驅動程序&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)。|  
    |*$phpType*[選用]|**SQLSRV_PHPTYPE_\*** 常數，可指定傳回值的 PHP 資料類型。<br /><br />如需 PHP 常數的詳細資訊，請參閱[常數 &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)。|  
    |*$sqlType*[選用]|**SQLSRV_SQLTYPE_\*** 常數，可指定輸入值的 SQL Server 資料類型。<br /><br />如需 PHP 常數的詳細資訊，請參閱[常數 &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)。|  
  
*$options* [選用]：設定查詢屬性的關聯陣列。 支援的索引鍵如下所示：  
  
|索引鍵|支援的值|Description|  
|-------|--------------------|---------------|  
|QueryTimeout|正整數值。|設定查詢逾時 (以秒為單位)。 根據預設，驅動程式會無限期等候結果。|  
|SendStreamParamsAtExec|**[True]** 或 **[False]**<br /><br />預設值為 **true**。|設定驅動程式在執行時傳送所有資料流資料 (**true**)，或是以區塊傳送資料流資料 (**false**)。 依預設，此值設定為 **true**。 如需詳細資訊，請參閱 [sqlsrv_send_stream_data](../../connect/php/sqlsrv-send-stream-data.md)。|  
|可捲動|SQLSRV_CURSOR_FORWARD<br /><br />SQLSRV_CURSOR_STATIC<br /><br />SQLSRV_CURSOR_DYNAMIC<br /><br />SQLSRV_CURSOR_KEYSET<br /><br />SQLSRV_CURSOR_CLIENT_BUFFERED|如需這些值的詳細資訊，請參閱 [指定資料指標類型及選取資料列](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md)。|  
  
## <a name="return-value"></a>傳回值  
陳述式資源。 如果無法建立且 (或) 無法執行陳述式，將會傳回 **false**。  
  
## <a name="remarks"></a>Remarks  
**sqlsrv_query** 函式非常適用於一次性查詢，且應作為執行查詢的預設選擇 (除非情況特殊)。 此函數提供簡便的方法，可用最少量的程式碼來執行查詢。 **sqlsrv_query** 函式可執行陳述式準備和陳述式執行，而且可用來執行參數化查詢。  
  
如需詳細資訊，請參閱 [How to: Retrieve Output Parameters Using the SQLSRV Driver](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)。  
  
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
> 建議使用字串做為輸入，繫結至的值時[十進位或數值資料行](https://docs.microsoft.com/sql/t-sql/data-types/decimal-and-numeric-transact-sql)若要確保精確性與正確性，如 PHP 有限精確度[浮點數](http://php.net/manual/en/language.types.float.php)。 這同樣適用於 bigint 資料行，尤其是值為範圍外[整數](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)。

## <a name="example"></a>範例  
此程式碼範例示範如何繫結十進位值做為輸入參數。  

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
此程式碼範例示範如何建立資料表[sql_variant](https://docs.microsoft.com/sql/t-sql/data-types/sql-variant-transact-sql)類型，並擷取插入的資料。

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

  
