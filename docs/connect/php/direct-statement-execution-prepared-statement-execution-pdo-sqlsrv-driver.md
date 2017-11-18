---
title: "陳述式的備妥的陳述式執行 PDO_SQLSRV 驅動程式的直接 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 05544ca6-1e07-486c-bf03-e8c2c25b3024
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 979a54ac3c6a381b89f150823489b793ef3e6af5
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="direct-statement-execution-and-prepared-statement-execution-in-the-pdosqlsrv-driver"></a>PDO_SQLSRV 驅動程式中的直接陳述式執行和已備妥的陳述式執行
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本主題討論如何使用 pdo:: SQLSRV_ATTR_DIRECT_QUERY 屬性來指定直接陳述式執行，而不是預設值，已備妥的陳述式執行。  當驅動程式會準備陳述式時，它可能會導致更好的效能如果陳述式將會執行一次使用 繫結的參數。  
  
## <a name="remarks"></a>備註  
如果您想要傳送[!INCLUDE[tsql](../../includes/tsql_md.md)]直接至伺服器的未經由驅動程式的陳述式準備的陳述式，您可以設定的 pdo:: SQLSRV_ATTR_DIRECT_QUERY 屬性[pdo:: setattribute](../../connect/php/pdo-setattribute.md) （或驅動程式選項傳遞給[Pdo:: __construct](../../connect/php/pdo-construct.md)) 或當您呼叫[pdo:: prepare](../../connect/php/pdo-prepare.md)。 根據預設，pdo:: SQLSRV_ATTR_DIRECT_QUERY 的值為 False （使用備妥的陳述式執行）。  
  
如果您使用[pdo:: query](../../connect/php/pdo-query.md)，您可以直接執行。 然後再呼叫[pdo:: query](../../connect/php/pdo-query.md)，呼叫[pdo:: setattribute](../../connect/php/pdo-setattribute.md)和 pdo:: SQLSRV_ATTR_DIRECT_QUERY 設為 True。  每次呼叫[pdo:: query](../../connect/php/pdo-query.md) pdo:: SQLSRV_ATTR_DIRECT_QUERY 可以為執行與不同的設定。  
  
如果您使用[pdo:: prepare](../../connect/php/pdo-prepare.md)和[pdostatement:: Execute](../../connect/php/pdostatement-execute.md)執行查詢多次使用繫結的參數，備妥的陳述式執行會進行最佳化查詢重複執行。  在此情況下，呼叫[pdo:: prepare](../../connect/php/pdo-prepare.md)使用 pdo:: SQLSRV_ATTR_DIRECT_QUERY 驅動程式的選項陣列參數中設定為 False。 必要時，您可以執行已備妥的陳述式以 pdo:: SQLSRV_ATTR_DIRECT_QUERY 設為 False。  
  
在您呼叫後[pdo:: prepare](../../connect/php/pdo-prepare.md)，pdo:: SQLSRV_ATTR_DIRECT_QUERY 的值執行備妥的查詢時，無法變更。  
  
如果查詢需要已在上一個查詢中設定的內容，您應該執行查詢以 pdo:: SQLSRV_ATTR_DIRECT_QUERY 設為 True。 例如，如果您在查詢中使用暫存資料表，pdo:: SQLSRV_ATTR_DIRECT_QUERY 必須設定為 True。  
  
下列範例會顯示需要從先前的陳述式的內容時，您需要將 pdo:: SQLSRV_ATTR_DIRECT_QUERY 設定為 True。  這個範例會使用直接執行查詢時，則只有在程式中的後續陳述式可以使用的暫存資料表。  
  
```  
<?php  
   $conn = new PDO('sqlsrv:Server=(local)', '', '');  
   $conn->setAttribute(constant('PDO::SQLSRV_ATTR_DIRECT_QUERY'), true);  
  
   $stmt1 = $conn->query("DROP TABLE #php_test_table");  
  
   $stmt2 = $conn->query("CREATE TABLE #php_test_table ([c1_int] int, [c2_int] int)");  
  
   $v1 = 1;  
   $v2 = 2;  
  
   $stmt3 = $conn->prepare("INSERT INTO #php_test_table (c1_int, c2_int) VALUES (:var1, :var2)");  
  
   if ($stmt3) {  
      $stmt3->bindValue(1, $v1);  
      $stmt3->bindValue(2, $v2);  
  
      if ($stmt3->execute())  
         echo "Execution succeeded\n";       
      else  
         echo "Execution failed\n";  
   }  
   else  
      var_dump($conn->errorInfo());  
  
   $stmt4 = $conn->query("DROP TABLE #php_test_table");  
?>  
```  
  
## <a name="see-also"></a>另請參閱  
[PHP SQL 驅動程式程式設計指南](../../connect/php/programming-guide-for-php-sql-driver.md)
  

