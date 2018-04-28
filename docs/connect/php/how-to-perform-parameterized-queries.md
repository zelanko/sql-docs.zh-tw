---
title: 如何： 執行參數化的查詢 |Microsoft 文件
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- updating data
- parameterized queries
ms.assetid: dc7d0ede-a9b6-4ce2-977e-4d1e7ec2131c
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0c6bc8d8ca5634a28992c24abf9281ff510d0238
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="how-to-perform-parameterized-queries"></a>如何：執行參數化查詢
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本主題摘要說明並示範如何使用 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 來執行參數化查詢。  
  
執行參數化查詢的步驟也可彙整成四個步驟：  
  
1.  將問號 (?) 當作參數預留位置放入即將執行查詢的 Transact-SQL 字串中。  
  
2.  初始化或更新對應至 Transact-SQL 查詢中預留位置的 PHP 變數。  
  
3.  使用步驟 2 中的 PHP 變數來建立或更新至 TRANSACT-SQL 字串中參數預留位置的對應參數值陣列。 陣列中的參數值必須是中的預留位置，代表它們的順序相同。
  
4.  執行查詢：  
  
    -   如果您使用 SQLSRV 驅動程式，請使用 [sqlsrv_query](../../connect/php/sqlsrv-query.md) 或 [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)/[sqlsrv_execute](../../connect/php/sqlsrv-execute.md)。  
  
    -   如果您使用 PDO_SQLSRV 驅動程式，以執行查詢[pdo:: prepare](../../connect/php/pdo-prepare.md)和[pdostatement:: Execute](../../connect/php/pdostatement-execute.md)。 [PDO::prepare](../../connect/php/pdo-prepare.md) 和 [PDOStatement::execute](../../connect/php/pdostatement-execute.md) 的主題有程式碼範例。  
  
本主題的其餘部分將討論使用 SQLSRV 驅動程式的參數化查詢。  
  
> [!NOTE]  
> 使用 **sqlsrv_prepare**。 這表示，如果使用 **sqlsrv_prepare** 準備參數化查詢並更新參數陣列中的值，則會在下次執行查詢時使用更新後的值。 如需詳細資訊，請參閱本主題中的第二個範例。  
  
## <a name="example"></a>範例  
下列範例會更新 AdventureWorks 資料庫的 *Production.ProductInventory* 資料表中指定產品識別碼的數量。 數量和產品識別碼都是 UPDATE 查詢中的參數。  
  
此範例會接著查詢資料庫，確認已正確更新數量。 產品識別碼是 SELECT 查詢中的參數。  
  
此範例假設 SQL Server 和[AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works)資料庫安裝在本機電腦上。 從命令列執行範例時，所有輸出都會寫入至主控台。  
  
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
  
/* Define the Transact-SQL query.  
Use question marks as parameter placeholders. */  
$tsql1 = "UPDATE Production.ProductInventory   
          SET Quantity = ?   
          WHERE ProductID = ?";  
  
/* Initialize $qty and $productId */  
$qty = 10; $productId = 709;  
  
/* Execute the statement with the specified parameter values. */  
$stmt1 = sqlsrv_query( $conn, $tsql1, array($qty, $productId));  
if( $stmt1 === false )  
{  
     echo "Statement 1 could not be executed.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Free statement resources. */  
sqlsrv_free_stmt( $stmt1);  
  
/* Now verify the updated quantity.  
Use a question mark as parameter placeholder. */  
$tsql2 = "SELECT Quantity   
          FROM Production.ProductInventory  
          WHERE ProductID = ?";  
  
/* Execute the statement with the specified parameter value.  
Display the returned data if no errors occur. */  
$stmt2 = sqlsrv_query( $conn, $tsql2, array($productId));  
if( $stmt2 === false )  
{  
     echo "Statement 2 could not be executed.\n";  
     die( print_r(sqlsrv_errors(), true));  
}  
else  
{  
     $qty = sqlsrv_fetch_array( $stmt2);  
     echo "There are $qty[0] of product $productId in inventory.\n";  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt2);  
sqlsrv_close( $conn);  
?>  
```  
  
前一個範例使用 **sqlsrv_query** 函數來執行查詢。 此函數非常適合用來執行一次性查詢，因為它會同時進行陳述式準備和執行。 組合**sqlsrv_prepare**/**sqlsrv_execute**最適合用於重新執行具有不同的參數值的查詢。 若要查看以不同的參數值重新執行查詢的範例，請參閱下一個範例。  
  
## <a name="example"></a>範例  
下列範例示範當您使用 **sqlsrv_prepare** 函數時如何隱含繫結變數。 此範例會將數個銷售訂單插入 *Sales.SalesOrderDetail* 資料表中。 *$Params*陣列都會繫結至陳述式 (*$stmt*) 時**sqlsrv_prepare**呼叫。 在每次執行可在資料表中插入新銷售訂單的查詢之前，都會以對應至銷售訂單詳細資料的新值來更新 *$params* 陣列。 後續的查詢執行會使用新的參數值。  
  
此範例假設 SQL Server 和[AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works)資料庫安裝在本機電腦上。 從命令列執行範例時，所有輸出都會寫入至主控台。  
  
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
  
$tsql = "INSERT INTO Sales.SalesOrderDetail (SalesOrderID,   
                                             OrderQty,   
                                             ProductID,   
                                             SpecialOfferID,   
                                             UnitPrice)  
         VALUES (?, ?, ?, ?, ?)";  
  
/* Each sub array here will be a parameter array for a query.  
The values in each sub array are, in order, SalesOrderID, OrderQty,  
 ProductID, SpecialOfferID, UnitPrice. */  
$parameters = array( array(43659, 8, 711, 1, 20.19),  
                     array(43660, 6, 762, 1, 419.46),  
                     array(43661, 4, 741, 1, 818.70)  
                    );  
  
/* Initialize parameter values. */  
$orderId = 0;  
$qty = 0;  
$prodId = 0;  
$specialOfferId = 0;  
$price = 0.0;  
  
/* Prepare the statement. $params is implicitly bound to $stmt. */  
$stmt = sqlsrv_prepare( $conn, $tsql, array( &$orderId,  
                                             &$qty,  
                                             &$prodId,  
                                             &$specialOfferId,  
                                             &$price));  
if( $stmt === false )  
{  
     echo "Statement could not be prepared.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Execute a statement for each set of params in $parameters.  
Because $params is bound to $stmt, as the values are changed, the  
new values are used in the subsequent execution. */  
foreach( $parameters as $params)  
{  
     list($orderId, $qty, $prodId, $specialOfferId, $price) = $params;  
     if( sqlsrv_execute($stmt) === false )  
     {  
          echo "Statement could not be executed.\n";  
          die( print_r( sqlsrv_errors(), true));  
     }  
     else  
     {  
          /* Verify that the row was successfully inserted. */  
          echo "Rows affected: ".sqlsrv_rows_affected( $stmt )."\n";  
     }  
}  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>另請參閱  
[轉換資料類型](../../connect/php/converting-data-types.md)

[安全性考量的 Microsoft Drivers for PHP for SQL Server](../../connect/php/security-considerations-for-php-sql-driver.md)

[關於文件中的程式碼範例](../../connect/php/about-code-examples-in-the-documentation.md)

[sqlsrv_rows_affected](../../connect/php/sqlsrv-rows-affected.md)  
  
