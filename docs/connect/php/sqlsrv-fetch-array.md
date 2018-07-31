---
title: sqlsrv_fetch_array |Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- sqlsrv_fetch_array
apitype: NA
helpviewer_keywords:
- sqlsrv_fetch_array
- retrieving data, as an array
- API Reference, sqlsrv_fetch_array
ms.assetid: 69270b9e-0791-42f4-856d-412da39dea63
caps.latest.revision: 52
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: aab41821d2f4eb1eb3f92ce998fe440593567d0a
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "37979711"
---
# <a name="sqlsrvfetcharray"></a>sqlsrv_fetch_array
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

將下一個資料列擷取為數值索引陣列和 (或) 關聯陣列。  
  
## <a name="syntax"></a>語法  
  
```  
  
sqlsrv_fetch_array( resource $stmt[, int $fetchType [, row[, ]offset]])  
```  
  
#### <a name="parameters"></a>參數  
*$stmt*：對應至執行之陳述式的陳述式資源。  
  
*$fetchType* [選擇性]：預先定義的常數。 此參數可以採用下表所列的其中一個值：  
  
|ReplTest1|Description|  
|---------|---------------|  
|SQLSRV_FETCH_NUMERIC|下一個資料列會以數值陣列的形式傳回。|  
|SQLSRV_FETCH_ASSOC|下一個資料列會以關聯陣列的形式傳回。 陣列索引鍵是結果集內的資料行名稱。|  
|SQLSRV_FETCH_BOTH|下一個資料列會同時以數值陣列和關聯陣列的形式傳回。 這是預設值。|  
  
*row* [選擇性]：在 1.1 版中新增。 下列其中一個值，指定要在使用可捲動資料指標的結果集內存取的資料列。 (如果指定 *row*，則必須明確指定 *fetchtype*，即使您指定預設值亦然。)  
  
-   SQLSRV_SCROLL_NEXT  
-   SQLSRV_SCROLL_PRIOR  
-   SQLSRV_SCROLL_FIRST  
-   SQLSRV_SCROLL_LAST  
-   SQLSRV_SCROLL_ABSOLUTE  
-   SQLSRV_SCROLL_RELATIVE  
  
如需這些值的詳細資訊，請參閱 [指定資料指標類型及選取資料列](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md)。 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]1.1 版已加入可捲動的資料指標支援。  
  
*offset* [選用]：與 SQLSRV_SCROLL_ABSOLUTE 和 SQLSRV_SCROLL_RELATIVE 搭配使用，以指定要擷取的資料列。 結果集內的第一個記錄為 0。  
  
## <a name="return-value"></a>傳回值  
如果擷取資料列，則會傳回 **陣列** 。 如果沒有更多資料列可擷取，則會傳回 **null** 。 若發生錯誤，將會傳回 **false** 。  
  
根據 *$fetchType* 參數的值，傳回的 **陣列** 可以是數值索引 **陣列**和 (或) 關聯 **陣列**。 根據預設，會傳回同時具有數值和關聯索引鍵的 **陣列** 。 傳回之陣列中的資料類型值，將是預設的 PHP 資料類型。 如需有關預設 PHP 資料類型的詳細資訊，請參閱 [Default PHP Data Types](../../connect/php/default-php-data-types.md)。  
  
## <a name="remarks"></a>Remarks  
如果傳回沒有名稱的資料行，則陣列元素的關聯索引鍵會是空字串 ("")。 例如，請考量下列將值插入資料庫資料表中，並擷取伺服器產生之主索引鍵的 Transact-SQL 陳述式：  
  
```
INSERT INTO Production.ProductPhoto (LargePhoto) VALUES (?);  
SELECT SCOPE_IDENTITY()
```
  
如果以關聯陣列的形式擷取此陳述式之 `SELECT SCOPE_IDENTITY()` 部分所傳回的結果集，傳回值的索引鍵將會是空字串 ("")，因為傳回的資料行沒有名稱。 若要避免此狀況，您可以用數值陣列的形式擷取結果，或是在 Transact-SQL 陳述式中為傳回的資料行指定名稱。 以下是在 Transact-SQL 中指定資料行名稱的方式之一：  
  
```
SELECT SCOPE_IDENTITY() AS PictureID
```
  
如果結果集包含多個沒有名稱的資料行，則最後一個未命名資料行的值將會指派給空字串 ("") 索引鍵。  
  
## <a name="example"></a>範例  
下列範例會以關聯 **陣列**的形式擷取結果集的每個資料列。 此範例假設本機電腦上已安裝 SQL Server 和 [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) 資料庫。 從命令列執行範例時，所有輸出都會寫入至主控台。  
  
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
  
/* Set up and execute the query. */  
$tsql = "SELECT FirstName, LastName  
         FROM Person.Contact  
         WHERE LastName='Alan'";  
$stmt = sqlsrv_query( $conn, $tsql);  
if( $stmt === false)  
{  
     echo "Error in query preparation/execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve each row as an associative array and display the results.*/  
while( $row = sqlsrv_fetch_array( $stmt, SQLSRV_FETCH_ASSOC))  
{  
      echo $row['LastName'].", ".$row['FirstName']."\n";  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="example"></a>範例  
下列範例會以數值索引陣列的形式擷取結果集的每個資料列。  
  
範例會針對具有指定的日期，以及存貨數量 (*StockQty*) 小於指定值的產品，從 AdventureWorks 資料庫的 *Purchasing.PurchaseOrderDetail* 資料表中擷取產品資訊。  
  
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
  
/* Define the query. */  
$tsql = "SELECT ProductID,  
                UnitPrice,  
                StockedQty   
         FROM Purchasing.PurchaseOrderDetail  
         WHERE StockedQty < 3   
         AND DueDate='2002-01-29'";  
  
/* Execute the query. */  
$stmt = sqlsrv_query( $conn, $tsql);  
if ( $stmt )  
{  
     echo "Statement executed.\n";  
}   
else   
{  
     echo "Error in statement execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Iterate through the result set printing a row of data upon each  
iteration.*/  
while( $row = sqlsrv_fetch_array( $stmt, SQLSRV_FETCH_NUMERIC))  
{  
     echo "ProdID: ".$row[0]."\n";  
     echo "UnitPrice: ".$row[1]."\n";  
     echo "StockedQty: ".$row[2]."\n";  
     echo "-----------------\n";  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
**sqlsrv_fetch_array** 函式一律會根據[預設 PHP 資料類型](../../connect/php/default-php-data-types.md)傳回資料。 如需如何指定 PHP 資料類型的相關資訊，請參閱 [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md)。  
  
如果擷取沒有名稱的欄位，則陣列元素的關聯索引鍵會是空字串 ("")。 如需詳細資訊，請參閱 [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md)。  
  
## <a name="see-also"></a>另請參閱  
[SQLSRV 驅動程式 API 參考](../../connect/php/sqlsrv-driver-api-reference.md)

[擷取資料](../../connect/php/retrieving-data.md)

[關於文件中的程式碼範例](../../connect/php/about-code-examples-in-the-documentation.md)

[適用於 SQL Server 程式設計適用於 PHP 的 Microsoft 驅動程式的指南](../../connect/php/programming-guide-for-php-sql-driver.md)
  
