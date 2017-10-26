---
title: "如何： 執行交易 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transaction support
ms.assetid: f4643b85-f929-4919-8951-23394bc5bfa7
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e24f0580fc79ab07043be419a866b19a47b80f73
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="how-to-perform-transactions"></a>如何：執行交易
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 的 SQLSRV 驅動程式提供三個函數來執行交易：  
  
-   [sqlsrv_begin_transaction](../../connect/php/sqlsrv-begin-transaction.md)  
  
-   [sqlsrv_commit](../../connect/php/sqlsrv-commit.md)  
  
-   [sqlsrv_rollback](../../connect/php/sqlsrv-rollback.md)  
  
PDO_SQLSRV 驅動程式提供三個方法來執行交易：  
  
-   [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md)  
  
-   [PDO::commit](../../connect/php/pdo-commit.md)  
  
-   [PDO::rollback](../../connect/php/pdo-rollback.md)  
  
如需範例，請參閱 [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) 。  
  
本主題的其餘部分說明並示範如何使用 SQLSRV 驅動程式來執行交易。  
  
## <a name="remarks"></a>備註  
執行交易的步驟可以摘要如下：  
  
1.  以 **sqlsrv_begin_transaction**開始交易。  
  
2.  檢查屬於交易的每個查詢成功或失敗。  
  
3.  如果適當，請以 **sqlsrv_commit**開始交易。 否則，請以 **sqlsrv_rollback**開始交易。 在呼叫**sqlsrv_commit**或**sqlsrv_rollback**，驅動程式會回到自動認可模式。  
  
    根據預設，[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]處於自動認可模式。 這表示所有查詢都會在成功時自動進行認可，除非已使用 **sqlsrv_begin_transaction**開始交易。  
  
    如果明確交易不是以 **sqlsrv_commit**來認可，它會在關閉連接或終止指令碼時復原。  
  
    請勿使用內嵌的 Transact-SQL 來執行交易。 例如，請勿執行以 "BEGIN TRANSACTION" 作為 Transact-SQL 查詢的陳述式，進而開始交易。 當您使用內嵌的 Transact-SQL 來執行交易時，無法保證預期的交易行為。  
  
    稍早所列的 **Sqlsrv** 函數應該用來執行交易。  
  
## <a name="example"></a>範例  
  
### <a name="description"></a>說明  
以下範例會在交易期間執行數個查詢。 如果所有查詢都成功，就會認可交易。 如果其中一個查詢失敗，則會復原交易。  
  
此範例會嘗試從 *Sales.SalesOrderDetail* 資料表刪除銷售訂單，並在銷售訂單中每項產品的 *Product.ProductInventory* 資料表中調整產品庫存量。 這些查詢會包含在交易中，因為對資料庫而言，所有查詢都必須成功，才能正確地反映訂單狀態和產品可用性。  
  
範例中的第一個查詢會擷取指定之銷售訂單識別碼的產品識別碼和數量。 此查詢不是交易的一部分。 不過，如果此查詢因為完成屬於後續交易一部分的查詢需有產品識別碼和數量而失敗，則指令碼會結束。  
  
這可確保查詢 (刪除銷售訂單和更新產品庫存量) 是交易的一部分。  
  
此範例假設本機電腦上已安裝 SQL Server 和 [AdventureWorks](http://go.microsoft.com/fwlink/?LinkID=67739) 資料庫。 從命令列執行範例時，所有輸出都會寫入至主控台。  
  
### <a name="code"></a>程式碼  
  
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
  
/* Begin transaction. */  
if( sqlsrv_begin_transaction($conn) === false )   
{   
     echo "Could not begin transaction.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Set the Order ID.  */  
$orderId = 43667;  
  
/* Execute operations that are part of the transaction. Commit on  
success, roll back on failure. */  
if (perform_trans_ops($conn, $orderId))  
{  
     //If commit fails, roll back the transaction.  
     if(sqlsrv_commit($conn))  
     {  
         echo "Transaction committed.\n";  
     }  
     else  
     {  
         echo "Commit failed - rolling back.\n";  
         sqlsrv_rollback($conn);  
     }  
}  
else  
{  
     "Error in transaction operation - rolling back.\n";  
     sqlsrv_rollback($conn);  
}  
  
/*Free connection resources*/  
sqlsrv_close( $conn);  
  
/*----------------  FUNCTION: perform_trans_ops  -----------------*/  
function perform_trans_ops($conn, $orderId)  
{  
    /* Define query to update inventory based on sales order info. */  
    $tsql1 = "UPDATE Production.ProductInventory   
              SET Quantity = Quantity + s.OrderQty   
              FROM Production.ProductInventory p   
              JOIN Sales.SalesOrderDetail s   
              ON s.ProductID = p.ProductID   
              WHERE s.SalesOrderID = ?";  
  
    /* Define the parameters array. */  
    $params = array($orderId);  
  
    /* Execute the UPDATE statement. Return false on failure. */  
    if( sqlsrv_query( $conn, $tsql1, $params) === false ) return false;  
  
    /* Delete the sales order. Return false on failure */  
    $tsql2 = "DELETE FROM Sales.SalesOrderDetail   
              WHERE SalesOrderID = ?";  
    if(sqlsrv_query( $conn, $tsql2, $params) === false ) return false;  
  
    /* Return true because all operations were successful. */  
    return true;  
}  
?>  
```  
  
### <a name="comments"></a>註解  
為了將焦點放在交易行為上，上述範例中並未包含一些建議的錯誤處理方式。 對於生產應用程式，我們建議檢查任何對 **sqlsrv** 函數的呼叫是否有錯誤並予以處理。  
  
## <a name="see-also"></a>另請參閱  
[更新資料 &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/updating-data-microsoft-drivers-for-php-for-sql-server.md)  
[交易 (Database Engine)](http://go.microsoft.com/fwlink/?LinkId=105862)  
[關於文件中的程式碼範例](../../connect/php/about-code-examples-in-the-documentation.md)  
  

