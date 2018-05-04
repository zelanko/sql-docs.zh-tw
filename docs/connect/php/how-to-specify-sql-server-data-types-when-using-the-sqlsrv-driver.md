---
title: 如何： 使用 SQLSRV 驅動程式時，指定 SQL Server 資料類型 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- converting data types
- streaming data
ms.assetid: 1fcf73cb-5634-4d89-948f-9326f1dbd030
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e0b3de78e464376095db1c582b1e5ebf638784a9
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-specify-sql-server-data-types-when-using-the-sqlsrv-driver"></a>如何：使用 SQLSRV 驅動程式指定 SQL Server 資料類型
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本主題示範如何使用 SQLSRV 驅動程式，為傳送到伺服器的資料指定 SQL Server 資料類型。 使用 PDO_SQLSRV 驅動程式時並不適用本主題。  
  
若要指定 SQL Server 資料類型，您在準備或執行會插入或更新資料的查詢時，必須使用選用 *$params* 陣列。 如需 *$params* 陣列之結構和語法的詳細資訊，請參閱 [sqlsrv_query](../../connect/php/sqlsrv-query.md) 或 [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)。  
  
下列步驟概述如何在將資料傳送至伺服器時指定 SQL Server 資料類型：  
  
> [!NOTE]  
> 如果指定 SQL Server 資料類型，則會使用預設類型。 如需預設 SQL Server 資料類型的相關資訊，請參閱 [Default SQL Server Data Types](../../connect/php/default-sql-server-data-types.md)。  
  
1.  定義會插入或更新資料的 Transact-SQL 查詢。 在查詢中，請使用問號 (?) 做為參數值的預留位置。  
  
2.  初始化或更新對應至 Transact-SQL 查詢中預留位置的 PHP 變數。  
  
3.  建構在準備或執行查詢時要使用的 *$params* 陣列。 請注意， *$params* 陣列的每個元素，在您指定 SQL Server 資料類型時也必須是陣列。  
  
4.  指定所需的 SQL Server 資料類型，使用適當的**SQLSRV_SQLTYPE_\*** 常數中的每個子陣列的第四個參數為 *$params*陣列。 如需完整的清單**SQLSRV_SQLTYPE_\*** 常數，請參閱 Sqltype 」 一節的[常數&#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)。 例如，在下方的程式碼中， *$changeDate*、 *$rate*和 *$payFrequency* 分別指定為 **$params**陣列中的 SQL Server 類型 **datetime**、 **money** 和 *tinyint* 。 由於未指定 *$employeeId* 的 SQL Server 類型，而且它初始化為整數，因此會使用預設的 SQL Server 類型 **integer** 。  
  
    ```  
    $employeeId = 5;  
    $changeDate = "2005-06-07";  
    $rate = 30;  
    $payFrequency = 2;  
    $params = array(  
                array($employeeId, null),  
                array($changeDate, null, null, SQLSRV_SQLTYPE_DATETIME),  
                array($rate, null, null, SQLSRV_SQLTYPE_MONEY),  
                array($payFrequency, null, null, SQLSRV_SQLTYPE_TINYINT)  
              );  
    ```  
  
## <a name="example"></a>範例  
下列範例會將資料插入*HumanResources.EmployeePayHistory* AdventureWorks 資料庫的資料表。 對於 *$changeDate*、 *$rate*和 *$payFrequency* 參數，會指定 SQL Server 類型。 對於 *$employeeId* 參數會使用預設 SQL Server 類型。 若要確認資料已成功插入，可以擷取和顯示相同的資料。  
  
這個範例假設 SQL Server 和[AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works)資料庫安裝在本機電腦上。 從命令列執行範例時，所有輸出都會寫入至主控台。  
  
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
  
/* Define the query. */  
$tsql1 = "INSERT INTO HumanResources.EmployeePayHistory (EmployeeID,  
                                                        RateChangeDate,  
                                                        Rate,  
                                                        PayFrequency)  
           VALUES (?, ?, ?, ?)";  
  
/* Construct the parameter array. */  
$employeeId = 5;  
$changeDate = "2005-06-07";  
$rate = 30;  
$payFrequency = 2;  
$params1 = array(  
               array($employeeId, null),  
               array($changeDate, null, null, SQLSRV_SQLTYPE_DATETIME),  
               array($rate, null, null, SQLSRV_SQLTYPE_MONEY),  
               array($payFrequency, null, null, SQLSRV_SQLTYPE_TINYINT)  
           );  
  
/* Execute the INSERT query. */  
$stmt1 = sqlsrv_query($conn, $tsql1, $params1);  
if( $stmt1 === false )  
{  
     echo "Error in execution of INSERT.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve the newly inserted data. */  
/* Define the query. */  
$tsql2 = "SELECT EmployeeID, RateChangeDate, Rate, PayFrequency  
          FROM HumanResources.EmployeePayHistory  
          WHERE EmployeeID = ? AND RateChangeDate = ?";  
  
/* Construct the parameter array. */  
$params2 = array($employeeId, $changeDate);  
  
/*Execute the SELECT query. */  
$stmt2 = sqlsrv_query($conn, $tsql2, $params2);  
if( $stmt2 === false )  
{  
     echo "Error in execution of SELECT.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve and display the results. */  
$row = sqlsrv_fetch_array( $stmt2 );  
if( $row === false )  
{  
     echo "Error in fetching data.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
echo "EmployeeID: ".$row['EmployeeID']."\n";  
echo "Change Date: ".date_format($row['RateChangeDate'], "Y-m-d")."\n";  
echo "Rate: ".$row['Rate']."\n";  
echo "PayFrequency: ".$row['PayFrequency']."\n";  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt($stmt1);  
sqlsrv_free_stmt($stmt2);  
sqlsrv_close($conn);  
?>  
```  
  
## <a name="see-also"></a>另請參閱  
[擷取資料](../../connect/php/retrieving-data.md)

[關於文件中的程式碼範例](../../connect/php/about-code-examples-in-the-documentation.md)

[如何：指定 PHP 資料類型](../../connect/php/how-to-specify-php-data-types.md)

[轉換資料類型](../../connect/php/converting-data-types.md)

[如何：使用內建的 UTF-8 支援傳送及擷取 UTF-8 資料](../../connect/php/how-to-send-and-retrieve-utf-8-data-using-built-in-utf-8-support.md)  
  
