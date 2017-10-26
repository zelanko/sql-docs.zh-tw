---
title: "sqlsrv_begin_transaction |Microsoft 文件"
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
- sqlsrv_begin_transaction
apitype: NA
helpviewer_keywords:
- sqlsrv_begin_transaction
- transaction support
- API Reference, sqlsrv_begin_transaction
ms.assetid: 0b223bc8-4047-4329-9cbf-d350ab0fb886
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b28185f3e858f30a9ff67c73381b0b9c4f07a028
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsrvbegintransaction"></a>sqlsrv_begin_transaction
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

在指定的連接上開始交易。 目前交易包含在指定的連接上呼叫 **sqlsrv_begin_transaction** 之後和呼叫 [sqlsrv_rollback](../../connect/php/sqlsrv-rollback.md) 或 [sqlsrv_commit](../../connect/php/sqlsrv-commit.md)之前執行的所有陳述式。  
  
> [!NOTE]  
> [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]處於依預設自動認可模式。 這表示所有查詢都會在成功時自動進行認可，除非已使用 **sqlsrv_begin_transaction**開始交易。  
  
> [!NOTE]  
> 如果**sqlsrv_begin_transaction**呼叫之後，交易已在連接上啟動，但未完成藉由呼叫**sqlsrv_commit**或**sqlsrv_rollback**，則會傳回呼叫**false**和*已在交易*錯誤加入至錯誤集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
sqlsrv_begin_transaction( resource $conn)  
```  
  
#### <a name="parameters"></a>參數  
*$conn*：與交易相關聯的連接。  
  
## <a name="return-value"></a>傳回值  
布林值：如果交易已成功開始，則傳回 **true** 。 否則為 **false**。  
  
## <a name="example"></a>範例  
以下範例會在交易期間執行兩個查詢。 如果這兩個查詢都成功，就會認可交易。 如果其中一個 (或兩個) 查詢失敗，則會復原交易。  
  
範例中的第一個查詢會將新的銷售訂單插入到 AdventureWorks 資料庫的 *Sales.SalesOrderDetail* 資料表中。 此訂單適用於具有產品識別碼 709 的五個產品單位。 第二個查詢可減少產品識別碼 709 的存貨數量 (五個單位)。 這些查詢會包含在交易中，因為對資料庫而言，這兩個查詢都必須成功，才能正確地反映訂單狀態和產品可用性。  
  
此範例假設本機電腦上已安裝 SQL Server 和 [AdventureWorks](http://go.microsoft.com/fwlink/?LinkID=67739) 資料庫。 從命令列執行範例時，所有輸出都會寫入至主控台。  
  
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
     die( print_r( sqlsrv_errors(), true ));  
}  
  
/* Initiate transaction. */  
/* Exit script if transaction cannot be initiated. */  
if ( sqlsrv_begin_transaction( $conn ) === false )  
{  
     echo "Could not begin transaction.\n";  
     die( print_r( sqlsrv_errors(), true ));  
}  
  
/* Initialize parameter values. */  
$orderId = 43659; $qty = 5; $productId = 709;  
$offerId = 1; $price = 5.70;  
  
/* Set up and execute the first query. */  
$tsql1 = "INSERT INTO Sales.SalesOrderDetail   
                     (SalesOrderID,   
                      OrderQty,   
                      ProductID,   
                      SpecialOfferID,   
                      UnitPrice)  
          VALUES (?, ?, ?, ?, ?)";  
$params1 = array( $orderId, $qty, $productId, $offerId, $price);  
$stmt1 = sqlsrv_query( $conn, $tsql1, $params1 );  
  
/* Set up and execute the second query. */  
$tsql2 = "UPDATE Production.ProductInventory   
          SET Quantity = (Quantity - ?)   
          WHERE ProductID = ?";  
$params2 = array($qty, $productId);  
$stmt2 = sqlsrv_query( $conn, $tsql2, $params2 );  
  
/* If both queries were successful, commit the transaction. */  
/* Otherwise, rollback the transaction. */  
if( $stmt1 && $stmt2 )  
{  
     sqlsrv_commit( $conn );  
     echo "Transaction was committed.\n";  
}  
else  
{  
     sqlsrv_rollback( $conn );  
     echo "Transaction was rolled back.\n";  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt1);  
sqlsrv_free_stmt( $stmt2);  
sqlsrv_close( $conn);  
?>  
```  
  
為了將焦點放在交易行為上，上述範例中並未包含一些建議的錯誤處理方式。 對於生產應用程式，建議檢查任何對 **sqlsrv** 函數的呼叫是否有錯誤並予以處理。  
  
> [!NOTE]  
> 請勿使用內嵌的 Transact-SQL 來執行交易。 例如，請勿執行以 "BEGIN TRANSACTION" 作為 Transact-SQL 查詢的陳述式，進而開始交易。 使用內嵌的 Transact-SQL 來執行交易時，無法保證預期的交易行為。  
  
## <a name="see-also"></a>另請參閱  
[SQLSRV 驅動程式 API 參考](../../connect/php/sqlsrv-driver-api-reference.md)  
[如何：執行交易](../../connect/php/how-to-perform-transactions.md)  
[PHP SQL 驅動程式概觀](../../connect/php/overview-of-the-php-sql-driver.md) 
  

