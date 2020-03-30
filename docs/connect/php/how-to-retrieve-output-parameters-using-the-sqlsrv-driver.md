---
title: 如何：使用 SQLSRV 驅動程式擷取輸出參數 | Microsoft Docs
ms.custom: ''
ms.date: 04/11/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- stored procedure support
ms.assetid: 1157bab7-6ad1-4bdb-a81c-662eea3e7fcd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: db1216f513f353a6c703805c7aabe7b8dd468115
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "67993396"
---
# <a name="how-to-retrieve-output-parameters-using-the-sqlsrv-driver"></a>如何：使用 SQLSRV 驅動程式擷取輸出參數
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本主題示範如何呼叫將其中一個參數定義為輸出參數的預存程序。 在擷取輸出或輸入/輸出參數時，必須先取用預存程序所傳回的所有結果，傳回的參數值才可供存取。  
  
> [!NOTE]  
> 初始化或更新為 **null**、 **DateTime**或資料流類型的變數，無法作為輸出參數。  
  
以 SQLSRV_SQLTYPE_VARCHAR('max') 之類的資料流類型做為輸出參數時，可能會發生資料截斷。 目前不支援以資料流類型做為輸出參數。 就非資料流類型而言，如果未指定輸出參數的長度，或指定的長度不足以用於輸出參數，則可能會發生資料截斷。  
  
## <a name="example-1"></a>範例 1
下列範例會呼叫一個預存程序，傳回指定員工的年度迄今銷售量。 PHP 變數 *$lastName* 是輸入參數， *$salesYTD* 則是輸出參數。  
  
> [!NOTE]  
> 將 *$salesYTD* 初始化為 0.0，會將傳回的 PHPTYPE 設為 **float**。 若要確保資料類型的完整性，應在呼叫預存程序之前初始化輸出參數，或應指定所需的 PHPTYPE。 如需指定 PHPTYPE 的相關資訊，請參閱 [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md)。  
  
由於預存程序僅傳回一個結果，因此在執行預存程序之後， *$salesYTD* 中隨即包含輸出參數的傳回值。  
  
> [!NOTE]  
> 使用標準語法呼叫預存程序，是建議的做法。 如需標準語法的詳細資訊，請參閱[呼叫預存程序](../../relational-databases/native-client-odbc-stored-procedures/calling-a-stored-procedure.md)。  
  
此範例假設本機電腦上已安裝 SQL Server 和 [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) 資料庫。 從命令列執行範例時，所有輸出都會寫入至主控台。  
  
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
  
/* Drop the stored procedure if it already exists. */  
$tsql_dropSP = "IF OBJECT_ID('GetEmployeeSalesYTD', 'P') IS NOT NULL  
                DROP PROCEDURE GetEmployeeSalesYTD";  
$stmt1 = sqlsrv_query( $conn, $tsql_dropSP);  
if( $stmt1 === false )  
{  
     echo "Error in executing statement 1.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Create the stored procedure. */  
$tsql_createSP = " CREATE PROCEDURE GetEmployeeSalesYTD  
                   @SalesPerson nvarchar(50),  
                   @SalesYTD money OUTPUT  
                   AS  
                   SELECT @SalesYTD = SalesYTD  
                   FROM Sales.SalesPerson AS sp  
                   JOIN HumanResources.vEmployee AS e   
                   ON e.EmployeeID = sp.SalesPersonID  
                   WHERE LastName = @SalesPerson";  
$stmt2 = sqlsrv_query( $conn, $tsql_createSP);  
if( $stmt2 === false )  
{  
     echo "Error in executing statement 2.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/*--------- The next few steps call the stored procedure. ---------*/  
  
/* Define the Transact-SQL query. Use question marks (?) in place of  
 the parameters to be passed to the stored procedure */  
$tsql_callSP = "{call GetEmployeeSalesYTD( ?, ? )}";  
  
/* Define the parameter array. By default, the first parameter is an  
INPUT parameter. The second parameter is specified as an OUTPUT  
parameter. Initializing $salesYTD to 0.0 sets the returned PHPTYPE to  
float. To ensure data type integrity, output parameters should be  
initialized before calling the stored procedure, or the desired  
PHPTYPE should be specified in the $params array.*/  
$lastName = "Blythe";  
$salesYTD = 0.0;  
$params = array(   
                 array($lastName, SQLSRV_PARAM_IN),  
                 array(&$salesYTD, SQLSRV_PARAM_OUT)  
               );  
  
/* Execute the query. */  
$stmt3 = sqlsrv_query( $conn, $tsql_callSP, $params);  
if( $stmt3 === false )  
{  
     echo "Error in executing statement 3.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Display the value of the output parameter $salesYTD. */  
echo "YTD sales for ".$lastName." are ". $salesYTD. ".";  
  
/*Free the statement and connection resources. */  
sqlsrv_free_stmt( $stmt1);  
sqlsrv_free_stmt( $stmt2);  
sqlsrv_free_stmt( $stmt3);  
sqlsrv_close( $conn);  
?>  
```  

> [!NOTE]
> 將輸出參數繫結至 bigint 類型時，如果值可能會超出某個[整數](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)的範圍，您必須將其 SQL 欄位類型指定為 SQLSRV_SQLTYPE_BIGINT。 否則，這可能會導致「值超出範圍」例外狀況。

## <a name="example-2"></a>範例 2
此程式碼範例示範如何將大型 bigint 值繫結為輸出參數。  

```
<?php
$serverName = "(local)";
$connectionInfo = array("Database"=>"testDB");  
$conn = sqlsrv_connect($serverName, $connectionInfo);  
if ($conn === false) {  
    echo "Could not connect.\n";  
    die(print_r(sqlsrv_errors(), true));  
}  

// Assume the stored procedure spTestProcedure exists, which retrieves a bigint value of some large number
// e.g. 9223372036854
$bigintOut = 0;
$outSql = "{CALL spTestProcedure (?)}";
$stmt = sqlsrv_prepare($conn, $outSql, array(array(&$bigintOut, SQLSRV_PARAM_OUT, null, SQLSRV_SQLTYPE_BIGINT)));
sqlsrv_execute($stmt);
echo "$bigintOut\n";   // Expect 9223372036854

sqlsrv_free_stmt($stmt);  
sqlsrv_close($conn);  

?>
```

## <a name="see-also"></a>另請參閱  
[如何：使用 SQLSRV 驅動程式指定參數方向](../../connect/php/how-to-specify-parameter-direction-using-the-sqlsrv-driver.md)

[如何：使用 SQLSRV 驅動程式擷取輸入和輸出參數](../../connect/php/how-to-retrieve-input-and-output-parameters-using-the-sqlsrv-driver.md)

[擷取資料](../../connect/php/retrieving-data.md)  
  
