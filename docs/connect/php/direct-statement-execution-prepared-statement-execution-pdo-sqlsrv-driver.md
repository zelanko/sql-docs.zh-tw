---
title: 直接陳述式已備妥陳述式執行 PDO_SQLSRV 驅動程式 |Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 05544ca6-1e07-486c-bf03-e8c2c25b3024
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 005a2c4b34c9aae2cfdfe4663cbfcbe06a68b81a
ms.sourcegitcommit: c1105ce638078d2c941cd656b34f78486e6b2d89
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 02/22/2019
ms.locfileid: "56676106"
---
# <a name="direct-statement-execution-and-prepared-statement-execution-in-the-pdosqlsrv-driver"></a>PDO_SQLSRV 驅動程式中的直接陳述式執行和已備妥的陳述式執行
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本主題討論如何使用 PDO::SQLSRV_ATTR_DIRECT_QUERY 屬性來指定直接陳述式執行，而不是預設值 ─ 已備妥的陳述式執行。 使用已備妥的陳述式可能導致較佳的效能，如果陳述式會執行一次使用 參數繫結。  
  
## <a name="remarks"></a>Remarks  
如果您想要傳送[!INCLUDE[tsql](../../includes/tsql-md.md)]直接對伺服器而不需要由驅動程式的陳述式準備的陳述式，您可以設定的 pdo:: SQLSRV_ATTR_DIRECT_QUERY 屬性[pdo:: setattribute](../../connect/php/pdo-setattribute.md) （或驅動程式選項傳遞至[Pdo:: __construct](../../connect/php/pdo-construct.md)) 或當您呼叫[pdo:: prepare](../../connect/php/pdo-prepare.md)。 根據預設，pdo:: SQLSRV_ATTR_DIRECT_QUERY 的值為 False （使用備妥的陳述式執行）。  
  
如果您使用[pdo:: query](../../connect/php/pdo-query.md)，您可以直接執行。 然後再呼叫[pdo:: query](../../connect/php/pdo-query.md)，呼叫[pdo:: setattribute](../../connect/php/pdo-setattribute.md) pdo:: SQLSRV_ATTR_DIRECT_QUERY 設為 True。  每次呼叫[pdo:: query](../../connect/php/pdo-query.md) pdo:: SQLSRV_ATTR_DIRECT_QUERY 可以為執行不同的設定。  
  
如果您使用[pdo:: prepare](../../connect/php/pdo-prepare.md)並[pdostatement:: Execute](../../connect/php/pdostatement-execute.md)執行多次的查詢會使用繫結的參數，備妥的陳述式執行最佳化執行重複的查詢。  在此情況下，呼叫[pdo:: prepare](../../connect/php/pdo-prepare.md)使用 pdo:: SQLSRV_ATTR_DIRECT_QUERY 的驅動程式的選項陣列參數中設定為 False。 如有必要，您可以執行已備妥的陳述式與 pdo:: SQLSRV_ATTR_DIRECT_QUERY 的設定為 False。  
  
在您呼叫後[pdo:: prepare](../../connect/php/pdo-prepare.md)，執行已備妥的查詢時，無法變更 pdo:: SQLSRV_ATTR_DIRECT_QUERY 的值。  
  
如果查詢需要已設定在上一個查詢中的內容，然後執行您的查詢使用 pdo:: SQLSRV_ATTR_DIRECT_QUERY 設為 True。 例如，如果您在查詢中使用暫存資料表，pdo:: SQLSRV_ATTR_DIRECT_QUERY 必須設定為 True。  
  
下列範例示範當需要時從上一個陳述式的內容，您需要將 pdo:: SQLSRV_ATTR_DIRECT_QUERY 設為 True。 這個範例會使用直接執行查詢時，則只能用於您的程式中的後續陳述式中的暫存資料表。  
  
> [!NOTE]
> 如果查詢是要叫用預存程序，而且使用此預存程序使用中的暫存資料表[pdo:: exec](../../connect/php/pdo-exec.md)改。

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
[適用於 SQL Server 程式設計適用於 PHP 的 Microsoft 驅動程式的指南](../../connect/php/programming-guide-for-php-sql-driver.md)
  
