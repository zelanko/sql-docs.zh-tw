---
title: sqlsrv_prepare |Microsoft 文件
ms.custom: ''
ms.date: 05/22/2018
ms.prod: sql
ms.prod_service: connectivity
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- sqlsrv_prepare
apitype: NA
helpviewer_keywords:
- executing queries
- API Reference, sqlsrv_prepare
- sqlsrv_prepare
ms.assetid: 8c74c697-3296-4f5d-8fb9-e361f53f19a6
caps.latest.revision: 52
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d05dadf16e96589c2f16b7d31580cab61650b9e6
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2018
ms.locfileid: "34563916"
---
# <a name="sqlsrvprepare"></a>sqlsrv_prepare
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

建立與指定的連接相關聯的陳述式資源。 此函數有助於您執行多個查詢。  
  
## <a name="syntax"></a>語法  
  
```  
  
sqlsrv_prepare(resource $conn, string $tsql [, array $params [, array $options]])  
```  
  
#### <a name="parameters"></a>參數  
*$conn*：與已建立的陳述式相關聯的連接資源。  
  
*$tsql*： 對應至建立的陳述式的 TRANSACT-SQL 運算式。  
  
*$params* [選用]:**陣列**對應到參數化查詢中的值。 陣列的每個元素可以是下列其中一項：
  
-   常值。  
  
-   PHP 變數的參考。  
  
-   具有下列結構的 **陣列** ：  
  
    ```  
    array(&$value [, $direction [, $phpType [, $sqlType]]])  
    ```  
  
    > [!NOTE]  
    > 傳遞做為查詢參數的變數應由參考傳遞，而不是由值傳遞。 例如，應傳遞 `&$myVariable` ，而不是 `$myVariable`。 執行具有 by-value 參數的查詢時，會引發 PHP 警告。  
  
    下表說明這些陣列元素：  
  
    |元素|描述|  
    |-----------|---------------|  
    |*&$value*|常值或 PHP 變數的參考。|  
    |*$direction*[選擇性]|下列其中一種**SQLSRV_PARAM_\*** 用來指出參數方向的常數： **SQLSRV_PARAM_IN**， **SQLSRV_PARAM_OUT**， **SQLSRV_PARAM_INOUT**。 預設值是**SQLSRV_PARAM_IN**。<br /><br />如需 PHP 常數的詳細資訊，請參閱[常數&#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)。|  
    |*$phpType*[OPTIONAL]|A **SQLSRV_PHPTYPE_\*** 指定 PHP 資料類型傳回值的常數。|  
    |*$sqlType*[OPTIONAL]|A **SQLSRV_SQLTYPE_\*** 指定輸入值的 SQL Server 資料類型的常數。|  
  
*$options* [選用]: 設定查詢屬性的關聯陣列。 下表列出支援的索引鍵和對應的值：  
  
|索引鍵|支援的值|描述|  
|-------|--------------------|---------------|  
|QueryTimeout|正整數值。|設定查詢逾時 (以秒為單位)。 根據預設，此驅動程式無限期地等候結果。|  
|SendStreamParamsAtExec|**[True]** 或 **[False]**<br /><br />預設值為 **true**。|設定要傳送所有的資料流資料執行的驅動程式 (**true**)，或以區塊傳送資料流資料 (**false**)。 依預設，此值設定為 **true**。 如需詳細資訊，請參閱 [sqlsrv_send_stream_data](../../connect/php/sqlsrv-send-stream-data.md)。|  
|可捲動|SQLSRV_CURSOR_FORWARD<br /><br />SQLSRV_CURSOR_STATIC<br /><br />SQLSRV_CURSOR_DYNAMIC<br /><br />SQLSRV_CURSOR_KEYSET<br /><br />SQLSRV_CURSOR_CLIENT_BUFFERED|如需這些值的詳細資訊，請參閱 [指定資料指標類型及選取資料列](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md)。|  
  
## <a name="return-value"></a>傳回值  
陳述式資源。 如果無法建立陳述式資源，將會傳回 **false** 。  
  
## <a name="remarks"></a>備註  
當您準備以變數做為參數的陳述式時，這些變數會繫結至陳述式。 這表示如果您更新變數的值，下一次執行陳述式時，就會以更新的參數值來執行。  
  
組合**sqlsrv_prepare**和**sqlsrv_execute**分隔陳述式準備和陳述式執行兩個函式呼叫，而且可用來執行參數化的查詢。 此函數非常適合用來執行陳述式多次 (每次執行時使用不同的參數值)。  
  
如需寫入和讀取大量資訊的替代策略，請參閱[批次的 SQL 陳述式](../../odbc/reference/develop-app/batches-of-sql-statements.md)和[BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md)。  
  
如需詳細資訊，請參閱 [How to: Retrieve Output Parameters Using the SQLSRV Driver](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)。  
  
## <a name="example"></a>範例  
下列範例會準備及執行陳述式。 當執行陳述式 (請參閱[sqlsrv_execute](../../connect/php/sqlsrv-execute.md))，更新中的欄位*Sales.SalesOrderDetail* AdventureWorks 資料庫的資料表。 此範例假設 SQL Server 和[AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works)資料庫安裝在本機電腦上。 從命令列執行範例時，所有輸出都會寫入至主控台。  
  
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
  
/* Set up Transact-SQL query. */  
$tsql = "UPDATE Sales.SalesOrderDetail   
         SET OrderQty = ?   
         WHERE SalesOrderDetailID = ?";  
  
/* Assign parameter values. */  
$param1 = 5;  
$param2 = 10;  
$params = array(&$param1, &$param2);  
  
/* Prepare the statement. */  
if ($stmt = sqlsrv_prepare($conn, $tsql, $params)) {
    echo "Statement prepared.\n";  
} else {  
    echo "Statement could not be prepared.\n";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
/* Execute the statement. */  
if (sqlsrv_execute($stmt)) {  
    echo "Statement executed.\n";  
} else {  
    echo "Statement could not be executed.\n";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
/* Free the statement and connection resources. */  
sqlsrv_free_stmt($stmt);  
sqlsrv_close($conn);  
?>  
```  
  
## <a name="example"></a>範例  
下列範例示範如何準備陳述式，然後以不同的參數值重新加以執行。 此範例會更新 AdventureWorks 資料庫中 *Sales.SalesOrderDetail* 資料表的 *OrderQty* 資料行。 更新執行之後，將會查詢資料庫以確認更新已成功。 此範例假設 SQL Server 和[AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works)資料庫安裝在本機電腦上。 從命令列執行範例時，所有輸出都會寫入至主控台。  
  
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
  
/* Define the parameterized query. */  
$tsql = "UPDATE Sales.SalesOrderDetail  
         SET OrderQty = ?  
         WHERE SalesOrderDetailID = ?";  
  
/* Initialize parameters and prepare the statement. Variables $qty  
and $id are bound to the statement, $stmt1. */  
$qty = 0; $id = 0;  
$stmt1 = sqlsrv_prepare($conn, $tsql, array(&$qty, &$id));  
if ($stmt1) {  
    echo "Statement 1 prepared.\n";  
} else {  
    echo "Error in statement preparation.\n";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
/* Set up the SalesOrderDetailID and OrderQty information. This array  
maps the order ID to order quantity in key=>value pairs. */  
$orders = array(1=>10, 2=>20, 3=>30);  
  
/* Execute the statement for each order. */  
foreach ($orders as $id => $qty) {  
    // Because $id and $qty are bound to $stmt1, their updated  
    // values are used with each execution of the statement.   
    if (sqlsrv_execute($stmt1) === false) {  
        echo "Error in statement execution.\n";  
        die(print_r(sqlsrv_errors(), true));  
    }  
}  
echo "Orders updated.\n";  
  
/* Free $stmt1 resources.  This allows $id and $qty to be bound to a different statement.*/  
sqlsrv_free_stmt($stmt1);  
  
/* Now verify that the results were successfully written by selecting   
the newly inserted rows. */  
$tsql = "SELECT OrderQty   
         FROM Sales.SalesOrderDetail   
         WHERE SalesOrderDetailID = ?";  
  
/* Prepare the statement. Variable $id is bound to $stmt2. */  
$stmt2 = sqlsrv_prepare($conn, $tsql, array(&$id));  
if ($stmt2) {  
    echo "Statement 2 prepared.\n";  
} else {  
    echo "Error in statement preparation.\n";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
/* Execute the statement for each order. */  
foreach (array_keys($orders) as $id)  
{  
    /* Because $id is bound to $stmt2, its updated value   
    is used with each execution of the statement. */  
    if (sqlsrv_execute($stmt2)) {  
        sqlsrv_fetch($stmt2);  
        $quantity = sqlsrv_get_field($stmt2, 0);  
        echo "Order $id is for $quantity units.\n";  
    } else {  
        echo "Error in statement execution.\n";  
        die(print_r(sqlsrv_errors(), true));  
    }  
}  
  
/* Free $stmt2 and connection resources. */  
sqlsrv_free_stmt($stmt2);  
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
$stmt = sqlsrv_prepare($conn, "INSERT INTO TestTable (DecimalCol) VALUES (?)", $params);
sqlsrv_execute($stmt);

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

[擷取資料](../../connect/php/retrieving-data.md)

[更新資料 &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/updating-data-microsoft-drivers-for-php-for-sql-server.md)

