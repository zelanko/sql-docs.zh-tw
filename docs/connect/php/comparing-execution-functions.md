---
title: 比較執行函數 |Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- executing queries
ms.assetid: 130fc0fd-87dd-46b2-918f-de9dc572c769
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f2b4d6c85c399589aae4eedbaade4bbdc4f70609
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67993738"
---
# <a name="comparing-execution-functions"></a>比較執行函數
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 提供了數個執行函數的選項。  

## <a name="sqlsrv-execution-functions"></a>SQLSRV 執行函數  
如果您使用 SQLSRV 驅動程式，請使用 [sqlsrv_query](../../connect/php/sqlsrv-query.md) 執行單一查詢，並使用 [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md) 與 [sqlsrv_execute](../../connect/php/sqlsrv-execute.md) 執行備妥的陳述式多次 (每次執行時使用不同的參數值)。  

## <a name="pdosqlsrv-execution-functions"></a>PDO_SQLSRV 執行函數 
如果您使用 PDO_SQLSRV 驅動程式，您可以透過下列其中一種方式來執行查詢：  
  
-   [PDO::exec](../../connect/php/pdo-exec.md)  
  
-   [PDO::query](../../connect/php/pdo-query.md)  
  
-   [PDO::prepare](../../connect/php/pdo-prepare.md) 與 [PDOStatement::execute](../../connect/php/pdostatement-execute.md)。  
  
## <a name="see-also"></a>另請參閱  
[SQLSRV 驅動程式 API 參考](../../connect/php/sqlsrv-driver-api-reference.md)

[PDO_SQLSRV 驅動程式參考](../../connect/php/pdo-sqlsrv-driver-reference.md)

[Microsoft Drivers for PHP for SQL Server 的程式設計指南](../../connect/php/programming-guide-for-php-sql-driver.md)
  
