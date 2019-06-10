---
title: 如何：使用 SQLSRV 驅動程式處理錯誤和警告 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- errors and warnings
ms.assetid: fa231d60-4c06-4137-89e8-097c28638c5d
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 18aef50a23c7452e371abb30e6897b3ec11b48f3
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66796106"
---
# <a name="how-to-handle-errors-and-warnings-using-the-sqlsrv-driver"></a>如何：使用 SQLSRV 驅動程式處理錯誤和警告
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

根據預設，SQLSRV 驅動程式會將警告視為錯誤；呼叫 **sqlsrv** 函式時若產生錯誤或警告，則會傳回 **false**。 本主題示範如何關閉此預設行為，以及如何個別處理警告和錯誤。  
  
> [!NOTE]  
> 將警告視為錯誤的預設行為有一些例外。 對應至 SQLSTATE 值 01000、01001、01003 和 01S02 的警告絕不會被視為錯誤。  
  
## <a name="example"></a>範例  
下列程式碼範例會使用兩個使用者定義函式 **DisplayErrors** 和 **DisplayWarnings** 來處理錯誤和警告。 此範例示範如何透過下列方式個別處理警告和錯誤：  
  
1.  關閉將警告視為錯誤的預設行為。  
  
2.  建立會更新員工休假時數，並將其餘休假時數傳回為輸出參數的預存程序。 當員工的可用休假時數小於零時，預存程序會顯示警告。  
  
3.  對每個員工呼叫此預存程序，以更新數名員工的休假時數，並顯示與任何發生的警告和錯誤相對應的訊息。  
  
4.  顯示每個員工的剩餘休假時數。  
  
在第一次呼叫 **sqlsrv** 函式 ([sqlsrv_configure](../../connect/php/sqlsrv-configure.md)) 時，會將警告視為錯誤。 警告會加入至錯誤集合，因此您無須個別檢查警告和錯誤。 不過，在後續呼叫 **sqlsrv** 函數時，警告將不會被視為錯誤，因此您必須明確檢查警告和錯誤。  
  
另外請注意，範例程式碼會在每次呼叫 **sqlsrv** 函數之後檢查錯誤。 此為建議的實務做法。  
  
此範例假設本機電腦上已安裝 SQL Server 和 [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) 資料庫。 從命令列執行範例時，所有輸出都會寫入至主控台。 針對 AdventureWorks 資料庫的新安裝執行範例時，會產生三個警告和兩個錯誤。 前兩個警告是在您連接到資料庫時所發出的標準警告。 第三個警告是因為員工的可用休假時數更新為小於零的值而發生的。 之所以發生錯誤，則是因為員工的可用休假時數更新為小於 -40 小時的值；這違反了資料表的條件約束。  
  
```  
<?php  
/* Turn off the default behavior of treating errors as warnings.  
Note: Turning off the default behavior is done here for demonstration  
purposes only. If setting the configuration fails, display errors and  
exit the script. */  
if( sqlsrv_configure("WarningsReturnAsErrors", 0) === false)  
{  
     DisplayErrors();  
     die;  
}  
  
/* Connect to the local server using Windows Authentication and   
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array("Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
  
/* If the connection fails, display errors and exit the script. */  
if( $conn === false )  
{  
     DisplayErrors();  
     die;  
}  
/* Display any warnings. */  
DisplayWarnings();  
  
/* Drop the stored procedure if it already exists. */  
$tsql1 = "IF OBJECT_ID('SubtractVacationHours', 'P') IS NOT NULL  
                DROP PROCEDURE SubtractVacationHours";  
$stmt1 = sqlsrv_query($conn, $tsql1);  
  
/* If the query fails, display errors and exit the script. */  
if( $stmt1 === false)  
{  
     DisplayErrors();  
     die;  
}  
/* Display any warnings. */  
DisplayWarnings();  
  
/* Free the statement resources. */  
sqlsrv_free_stmt( $stmt1 );  
  
/* Create the stored procedure. */  
$tsql2 = "CREATE PROCEDURE SubtractVacationHours  
                  @EmployeeID int,  
                  @VacationHours smallint OUTPUT  
              AS  
                  UPDATE HumanResources.Employee  
                  SET VacationHours = VacationHours - @VacationHours  
                  WHERE EmployeeID = @EmployeeID;  
                  SET @VacationHours = (SELECT VacationHours    
                                       FROM HumanResources.Employee  
                                       WHERE EmployeeID = @EmployeeID);  
              IF @VacationHours < 0   
              BEGIN  
                PRINT 'WARNING: Vacation hours are now less than zero.'  
              END;";  
$stmt2 = sqlsrv_query( $conn, $tsql2 );  
  
/* If the query fails, display errors and exit the script. */  
if( $stmt2 === false)  
{  
     DisplayErrors();  
     die;  
}  
/* Display any warnings. */  
DisplayWarnings();  
  
/* Free the statement resources. */  
sqlsrv_free_stmt( $stmt2 );  
  
/* Set up the array that maps employee ID to used vacation hours. */  
$emp_hrs = array (7=>4, 8=>5, 9=>8, 11=>50);  
  
/* Initialize variables that will be used as parameters. */  
$employeeId = 0;  
$vacationHrs = 0;  
  
/* Set up the parameter array. */  
$params = array(  
                 array(&$employeeId, SQLSRV_PARAM_IN),  
                 array(&$vacationHrs, SQLSRV_PARAM_INOUT)  
                );  
  
/* Define and prepare the query to substract used vacation hours. */  
$tsql3 = "{call SubtractVacationHours(?, ?)}";  
$stmt3 = sqlsrv_prepare($conn, $tsql3, $params);  
  
/* If the statement preparation fails, display errors and exit the script. */  
if( $stmt3 === false)  
{  
     DisplayErrors();  
     die;  
}  
/* Display any warnings. */  
DisplayWarnings();  
  
/* Loop through the employee=>vacation hours array. Update parameter  
 values before statement execution. */  
foreach(array_keys($emp_hrs) as $employeeId)  
{  
     $vacationHrs = $emp_hrs[$employeeId];  
     /* Execute the query.  If it fails, display the errors. */  
     if( sqlsrv_execute($stmt3) === false)  
     {  
          DisplayErrors();  
          die;  
     }  
     /* Display any warnings. */  
     DisplayWarnings();  
  
     /*Move to the next result returned by the stored procedure. */  
     if( sqlsrv_next_result($stmt3) === false)  
     {  
          DisplayErrors();  
          die;  
     }  
     /* Display any warnings. */  
     DisplayWarnings();  
  
     /* Display updated vacation hours. */  
     echo "EmployeeID $employeeId has $vacationHrs ";  
     echo "remaining vacation hours.\n";  
}  
  
/* Free the statement and connection resources. */  
sqlsrv_free_stmt( $stmt3 );  
sqlsrv_close( $conn );  
  
/* ------------- Error Handling Functions --------------*/  
function DisplayErrors()  
{  
     $errors = sqlsrv_errors(SQLSRV_ERR_ERRORS);  
     foreach( $errors as $error )  
     {  
          echo "Error: ".$error['message']."\n";  
     }  
}  
  
function DisplayWarnings()  
{  
     $warnings = sqlsrv_errors(SQLSRV_ERR_WARNINGS);  
     if(!is_null($warnings))  
     {  
          foreach( $warnings as $warning )  
          {  
               echo "Warning: ".$warning['message']."\n";  
          }  
     }  
}  
?>  
```  
  
## <a name="see-also"></a>另請參閱  
[如何：使用 SQLSRV 驅動程式設定錯誤和警告處理](../../connect/php/how-to-configure-error-and-warning-handling-using-the-sqlsrv-driver.md)

[SQLSRV 驅動程式 API 參考](../../connect/php/sqlsrv-driver-api-reference.md)  
  
