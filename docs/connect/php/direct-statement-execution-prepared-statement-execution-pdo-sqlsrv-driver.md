---
title: Direct 語句-備妥的語句執行 PDO_SQLSRV 驅動程式 |Microsoft Docs
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
ms.openlocfilehash: fa9e544fb7b79009d86a5742946a722d5adc18f2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67993616"
---
# <a name="direct-statement-execution-and-prepared-statement-execution-in-the-pdosqlsrv-driver"></a>PDO_SQLSRV 驅動程式中的直接陳述式執行和已備妥的陳述式執行
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本主題討論如何使用 PDO::SQLSRV_ATTR_DIRECT_QUERY 屬性來指定直接陳述式執行，而不是預設值 ─ 已備妥的陳述式執行。 如果使用參數系結多次執行語句, 使用備妥的語句可能會產生較佳的效能。  
  
## <a name="remarks"></a>備註  
如果您想要在沒有[!INCLUDE[tsql](../../includes/tsql-md.md)]驅動程式準備的情況下將語句直接傳送到伺服器, 您可以使用[pdo:: setAttribute](../../connect/php/pdo-setattribute.md)來設定 pdo:: SQLSRV_ATTR_DIRECT_QUERY 屬性 (或作為傳遞至[pdo:: __construct 的驅動程式選項)。](../../connect/php/pdo-construct.md)) 或當您呼叫[PDO::p 準備](../../connect/php/pdo-prepare.md)時。 根據預設, PDO:: SQLSRV_ATTR_DIRECT_QUERY 的值為 False (使用備妥的語句執行)。  
  
如果您使用[PDO:: query](../../connect/php/pdo-query.md), 您可能會想要直接執行。 呼叫[pdo:: query](../../connect/php/pdo-query.md)之前, 請呼叫[Pdo:: setAttribute](../../connect/php/pdo-setattribute.md) , 並將 pdo:: SQLSRV_ATTR_DIRECT_QUERY 設定為 True。  [Pdo:: query](../../connect/php/pdo-query.md)的每次呼叫都可以使用 pdo:: SQLSRV_ATTR_DIRECT_QUERY 的不同設定來執行。  
  
如果您使用[PDO::p 準備](../../connect/php/pdo-prepare.md)和[PDOStatement:: execute](../../connect/php/pdostatement-execute.md) , 使用系結參數多次執行查詢, 備妥的語句執行會優化重複查詢的執行。  在此情況下, 請在驅動程式選項陣列參數中, 將 pdo:: SQLSRV_ATTR_DIRECT_QUERY 設定為 False, 以呼叫[pdo::p 準備](../../connect/php/pdo-prepare.md)。 必要時, 您可以使用 PDO:: SQLSRV_ATTR_DIRECT_QUERY 設定為 False 來執行備妥的語句。  
  
在您呼叫[pdo::p 準備](../../connect/php/pdo-prepare.md)之後, 在執行備妥的查詢時, PDO:: SQLSRV_ATTR_DIRECT_QUERY 的值就不能變更。  
  
如果查詢需要在上一個查詢中設定的內容, 請使用將 PDO:: SQLSRV_ATTR_DIRECT_QUERY 設定為 True 來執行查詢。 例如, 如果您在查詢中使用臨時表, PDO:: SQLSRV_ATTR_DIRECT_QUERY 必須設定為 True。  
  
下列範例顯示當需要來自前一個語句的內容時, 您必須將 PDO:: SQLSRV_ATTR_DIRECT_QUERY 設定為 True。 這個範例使用臨時表, 只有在直接執行查詢時, 程式中的後續語句才可使用。  
  
> [!NOTE]
> 如果查詢是用來叫用預存程式, 而且此預存程式中使用臨時表, 請改用[PDO:: exec](../../connect/php/pdo-exec.md) 。

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
[Microsoft Drivers for PHP for SQL Server 的程式設計指南](../../connect/php/programming-guide-for-php-sql-driver.md)
  
