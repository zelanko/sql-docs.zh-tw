---
title: 直接陳述式 - 已備妥的陳述式執行 PDO_SQLSRV 驅動程式 | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 05544ca6-1e07-486c-bf03-e8c2c25b3024
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1ca9ab0e2846ddff98b6a0d7b626ae6757517a2d
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80928002"
---
# <a name="direct-statement-execution-and-prepared-statement-execution-in-the-pdo_sqlsrv-driver"></a>PDO_SQLSRV 驅動程式中的直接陳述式執行和已備妥的陳述式執行
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本主題討論如何使用 PDO::SQLSRV_ATTR_DIRECT_QUERY 屬性來指定直接陳述式執行，而不是預設值 ─ 已備妥的陳述式執行。 如果使用參數繫結多次執行陳述式，使用備妥的陳述式可能會產生較佳的效能。  
  
## <a name="remarks"></a>備註  
若要將 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式直接傳送至伺服器，但不含驅動程式備妥的陳述式，您可以使用 [PDO::setAttribute](../../connect/php/pdo-setattribute.md) (或是傳遞至 [PDO::__construct](../../connect/php/pdo-construct.md) 的驅動程式選項)，或在呼叫 [PDO::prepare](../../connect/php/pdo-prepare.md) 時，設定 PDO::SQLSRV_ATTR_DIRECT_QUERY 屬性。 根據預設，PDO::SQLSRV_ATTR_DIRECT_QUERY 的值為 False (使用備妥的陳述式執行)。  
  
如果您使用 [PDO::query](../../connect/php/pdo-query.md)，您可能會想要直接執行。 在呼叫 [PDO::query](../../connect/php/pdo-query.md) 之前，請先呼叫 [PDO::setAttribute](../../connect/php/pdo-setattribute.md) 並將 PDO::SQLSRV_ATTR_DIRECT_QUERY 設定為 True。  [PDO::query](../../connect/php/pdo-query.md) 的每個呼叫都可以使用 PDO::SQLSRV_ATTR_DIRECT_QUERY 的不同設定來執行。  
  
如果您使用 [PDO::prepare](../../connect/php/pdo-prepare.md) 和 [PDOStatement::execute](../../connect/php/pdostatement-execute.md) 使用繫結參數多次執行查詢，備妥的陳述式執行會最佳化重複查詢的執行。  在此情況下，請在驅動程式選項陣列參數中將 PDO::SQLSRV_ATTR_DIRECT_QUERY 設定為 False 的情況下呼叫 [PDO::prepare](../../connect/php/pdo-prepare.md)。 必要時，您可以在 PDO::SQLSRV_ATTR_DIRECT_QUERY 設定為 False 的情況下執行備妥的陳述式。  
  
在您呼叫 [PDO::prepare](../../connect/php/pdo-prepare.md) 之後，在執行備妥的查詢時，PDO::SQLSRV_ATTR_DIRECT_QUERY 的值就不能變更。  
  
如果查詢需要先前查詢中所設定的內容，請在 PDO::SQLSRV_ATTR_DIRECT_QUERY 設定為 True 的情況下來執行查詢。 例如，如果您在查詢中使用暫存資料表，則 PDO::SQLSRV_ATTR_DIRECT_QUERY 必須設定為 True。  
  
下列範例顯示當需要上一個陳述式的上下文時，您必須將 PDO::SQLSRV_ATTR_DIRECT_QUERY 設定為 True。 這個範例使用暫存資料表，這些暫存資料表僅在直接執行查詢時才可用於程式中的後續陳述式。  
  
> [!NOTE]
> 如果查詢是用來叫用預存程序，而且此預存程序中使用暫存資料表，請改為使用 [PDO::exec](../../connect/php/pdo-exec.md)。

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
  
