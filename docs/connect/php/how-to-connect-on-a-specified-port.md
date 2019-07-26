---
title: '如何: 在指定的埠上連接 |Microsoft Docs'
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to the server, specifying a port
ms.assetid: 65a154d1-375c-439b-a653-7815c9d70ff3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: af055a73904bb8feec92fb2afe93df064a09ab23
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015047"
---
# <a name="how-to-connect-on-a-specified-port"></a>如何：在指定的通訊埠上連接
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本主題說明如何透過 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]在指定的通訊埠上連接到 SQL Server。  
  
### <a name="to-connect-on-a-specified-port"></a>在指定的通訊埠上連接  
  
1.  驗證伺服器設定為接受連接的通訊埠。 如需將伺服器設定為在指定的連接埠上接受連線的資訊，請參閱[設定伺服器接聽特定 TCP 通訊埠 (SQL Server 設定管理員)](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md)。  
  
2.  將所需的連接埠新增至 [sqlsrv_connect](../../connect/php/sqlsrv-connect.md) 函式的 *$serverName* 參數。 請以逗號分隔伺服器名稱和通訊埠。 例如，下列程式碼行會使用 SQLSRV 驅動程式示範如何在通訊埠 1521 上連接到名為 *myServer* 的伺服器：  
  
    ```  
    $serverName = "myServer, 1521";  
    sqlsrv_connect( $serverName );  
    ```  
  
    下列程式碼行會使用 PDO_SQLSRV 驅動程式示範如何在連接埠 1521 上連線到名為 *myServer* 的伺服器：  
  
    ```  
    $serverName = "(local), 1521";  
    $database = "AdventureWorks";  
    $conn = new PDO( "sqlsrv:server=$serverName;Database=$database", "", "");  
    ```  
  
## <a name="see-also"></a>另請參閱  
[連線到伺服器](../../connect/php/connecting-to-the-server.md)

[Microsoft Drivers for PHP for SQL Server 的程式設計指南](../../connect/php/programming-guide-for-php-sql-driver.md)

[開始使用 Microsoft Drivers for PHP for SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[SQLSRV 驅動程式 API 參考](../../connect/php/sqlsrv-driver-api-reference.md)

[PDO_SQLSRV 驅動程式參考](../../connect/php/pdo-sqlsrv-driver-reference.md)  
  
