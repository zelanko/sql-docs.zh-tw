---
title: "如何： 指定的通訊埠上連接 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: connecting to the server, specifying a port
ms.assetid: 65a154d1-375c-439b-a653-7815c9d70ff3
caps.latest.revision: "20"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c8f5fcabd257f602c9ceba97806b031e95142a76
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="how-to-connect-on-a-specified-port"></a>如何：在指定的通訊埠上連接
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本主題說明如何透過 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]在指定的通訊埠上連接到 SQL Server。  
  
### <a name="to-connect-on-a-specified-port"></a>在指定的通訊埠上連接  
  
1.  驗證伺服器設定為接受連接的通訊埠。 如需設定伺服器，以接受指定的連接埠上連接資訊，請參閱[How to： 設定伺服器接聽特定 TCP 通訊埠 （SQL Server 組態管理員）](http://go.microsoft.com/fwlink/?LinkId=121865)。  
  
2.  加入所需的連接埠*$serverName*參數[sqlsrv_connect](../../connect/php/sqlsrv-connect.md)函式。 請以逗號分隔伺服器名稱和通訊埠。 例如，下列程式碼行會使用 SQLSRV 驅動程式示範如何在通訊埠 1521 上連接到名為 *myServer* 的伺服器：  
  
    ```  
    $serverName = "myServer, 1521";  
    sqlsrv_connect( $serverName );  
    ```  
  
    下列程式碼使用 PDO_SQLSRV 驅動程式示範如何連接到伺服器，名稱為*myServer*通訊埠 1521年上：  
  
    ```  
    $serverName = "(local), 1521";  
    $database = "AdventureWorks";  
    $conn = new PDO( "sqlsrv:server=$serverName;Database=$database", "", "");  
    ```  
  
## <a name="see-also"></a>請參閱＜  
[連接到伺服器](../../connect/php/connecting-to-the-server.md)  
[PHP SQL 驅動程式程式設計指南](../../connect/php/programming-guide-for-php-sql-driver.md)
[PHP SQL 驅動程式快速入門](../../connect/php/getting-started-with-the-php-sql-driver.md) 
[SQLSRV 驅動程式 API 參考](../../connect/php/sqlsrv-driver-api-reference.md)  
[PDO_SQLSRV 驅動程式參考](../../connect/php/pdo-sqlsrv-driver-reference.md)  
  
