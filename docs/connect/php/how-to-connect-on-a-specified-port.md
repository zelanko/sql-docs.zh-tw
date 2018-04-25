---
title: 如何： 指定的通訊埠上連接 |Microsoft 文件
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- connecting to the server, specifying a port
ms.assetid: 65a154d1-375c-439b-a653-7815c9d70ff3
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b17dd2bb8df3f7274cb8eea36faf3ee5f320f983
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MTE
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="how-to-connect-on-a-specified-port"></a>如何：在指定的通訊埠上連接
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本主題說明如何透過 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]在指定的通訊埠上連接到 SQL Server。  
  
### <a name="to-connect-on-a-specified-port"></a>在指定的通訊埠上連接  
  
1.  驗證伺服器設定為接受連接的通訊埠。 如需將伺服器設定為在指定的通訊埠上接受連接的資訊，請參閱[如何：設定伺服器接聽特定 TCP 通訊埠 ](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md)SQL Server 組態管理員。  
  
2.  將所需的通訊埠加入 *$serverName* parameter of the [sqlsrv](../../connect/php/sqlsrv-connect.md)connect 函數。 請以逗號分隔伺服器名稱和通訊埠。 例如，下列程式碼行會使用 SQLSRV 驅動程式示範如何在通訊埠 1521 上連接到名為 *myServer* 的伺服器：  
  
    ```  
    $serverName = "myServer, 1521";  
    sqlsrv_connect( $serverName );  
    ```  
  
    下列程式碼行會使用 PDO*SQLSRV 驅動程式示範如何在通訊埠 1521 上連接到名為* myServer 的伺服器：  
  
    ```  
    $serverName = "(local), 1521";  
    $database = "AdventureWorks";  
    $conn = new PDO( "sqlsrv:server=$serverName;Database=$database", "", "");  
    ```  
  
## <a name="see-also"></a>另請參閱  
[連線到伺服器](../../connect/php/connecting-to-the-server.md)

[程式程式設計指南 Microsoft Drivers for PHP，適用於 SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)

[開始使用 Microsoft Drivers for PHP for SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[SQLSRV 驅動程式 API 參考](../../connect/php/sqlsrv-driver-api-reference.md)

[PDO_SQLSRV 驅動程式參考](../../connect/php/pdo-sqlsrv-driver-reference.md)  
  
