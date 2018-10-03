---
title: sqlsrv_cancel |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_cancel
apitype: NA
helpviewer_keywords:
- sqlsrv_cancel
- API Reference, sqlsrv_cancel
ms.assetid: 75798c9b-f711-445d-9b8f-ba4d405ca50a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ad06888895e863760cfde3589475a230e33f9a06
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47615256"
---
# <a name="sqlsrvcancel"></a>sqlsrv_cancel
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

取消陳述式。 這表示會捨棄陳述式的任何擱置結果。 在呼叫此函式後，如果陳述式已透過 [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md) 備妥，則可以重新執行該陳述式。 如果已取用所有與陳述式相關聯的結果，則不需要呼叫此函數。  
  
## <a name="syntax"></a>語法  
  
```  
  
sqlsrv_cancel( resource $stmt)  
```  
  
#### <a name="parameters"></a>參數  
*$stmt*：要取消的陳述式。  
  
## <a name="return-value"></a>傳回值  
布林值：如果作業成功，則為 **true** 。 否則為 **false**。  
  
## <a name="example"></a>範例  
下列範例會以 [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) 資料庫作為執行查詢的目標，然後取用並計算結果，直到變數 *$salesTotal* 達到指定的數量。 然後會捨棄其餘的查詢結果。 此範例假設本機電腦上已安裝 SQL Server 和 AdventureWorks 資料庫。 從命令列執行範例時，所有輸出都會寫入至主控台。  
  
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
  
/* Prepare and execute the query. */  
$tsql = "SELECT OrderQty, UnitPrice FROM Sales.SalesOrderDetail";  
$stmt = sqlsrv_prepare( $conn, $tsql);  
if( $stmt === false )  
{  
     echo "Error in statement preparation.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
if( sqlsrv_execute( $stmt ) === false)  
{  
     echo "Error in statement execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Initialize tracking variables. */  
$salesTotal = 0;  
$count = 0;  
  
/* Count and display the number of sales that produce revenue  
of $100,000. */  
while( ($row = sqlsrv_fetch_array( $stmt)) && $salesTotal <=100000)  
{  
     $qty = $row[0];  
     $price = $row[1];  
     $salesTotal += ( $price * $qty);  
     $count++;  
}  
echo "$count sales accounted for the first $$salesTotal in revenue.\n";  
  
/* Cancel the pending results. The statement can be reused. */  
sqlsrv_cancel( $stmt);  
?>  
```  
  
## <a name="comments"></a>註解  
已使用 [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md) 與 [sqlsrv_execute](../../connect/php/sqlsrv-execute.md) 的組合備妥並執行的陳述式，可在呼叫 **sqlsrv_cancel** 之後透過 **sqlsrv_execute** 重新執行。 透過 [sqlsrv_query](../../connect/php/sqlsrv-query.md) 執行的陳述式，則無法在呼叫 **sqlsrv_cancel** 之後重新執行。  
  
## <a name="see-also"></a>另請參閱  
[SQLSRV 驅動程式 API 參考](../../connect/php/sqlsrv-driver-api-reference.md)

[連線到伺服器](../../connect/php/connecting-to-the-server.md)

[擷取資料](../../connect/php/retrieving-data.md)

[關於文件中的程式碼範例](../../connect/php/about-code-examples-in-the-documentation.md)

[sqlsrv_free_stmt](../../connect/php/sqlsrv-free-stmt.md)

  
