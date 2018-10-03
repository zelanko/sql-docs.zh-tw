---
title: 比較執行函式 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 46a1f3e53c4953f08400d5d5599bec348fb6b15c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47749434"
---
# <a name="comparing-execution-functions"></a>比較執行函數
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 提供了數個執行函數的選項。  

## <a name="sqlsrv-execution-functions"></a>SQLSRV 執行函式  
如果您使用 SQLSRV 驅動程式，請使用 [sqlsrv_query](../../connect/php/sqlsrv-query.md) 執行單一查詢，並使用 [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md) 與 [sqlsrv_execute](../../connect/php/sqlsrv-execute.md) 執行備妥的陳述式多次 (每次執行時使用不同的參數值)。  

## <a name="pdosqlsrv-execution-functions"></a>PDO_SQLSRV 執行函式 
如果您使用 PDO_SQLSRV 驅動程式，您可以透過下列其中一種方式來執行查詢：  
  
-   [PDO::exec](../../connect/php/pdo-exec.md)  
  
-   [PDO::query](../../connect/php/pdo-query.md)  
  
-   [PDO::prepare](../../connect/php/pdo-prepare.md) 與 [PDOStatement::execute](../../connect/php/pdostatement-execute.md)。  
  
## <a name="see-also"></a>另請參閱  
[SQLSRV 驅動程式 API 參考](../../connect/php/sqlsrv-driver-api-reference.md)

[PDO_SQLSRV 驅動程式參考](../../connect/php/pdo-sqlsrv-driver-reference.md)

[適用於 SQL Server 程式設計適用於 PHP 的 Microsoft 驅動程式的指南](../../connect/php/programming-guide-for-php-sql-driver.md)
  
