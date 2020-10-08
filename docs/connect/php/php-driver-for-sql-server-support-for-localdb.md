---
title: PHP 驅動程式對 LocalDB 的支援
description: 了解 Microsoft PHP Driver for SQL Server 如何支援到 LocalDB 資料庫執行個體的連線。
ms.custom: ''
ms.date: 05/06/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d315ad6a-0d50-4093-80c2-2f11217237c2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 47bcfa16712e0ef227da7c7ae53de14aa42deacb
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726769"
---
# <a name="support-for-localdb"></a>LocalDB 的支援

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

LocalDB 是輕量版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，從 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 開始提供。 本主題將討論如何連接到 LocalDB 執行個體中的資料庫。

## <a name="remarks"></a>備註

如需 LocalDB 的詳細資訊，包括如何安裝 LocalDB 和設定 LocalDB 執行個體，請參閱有關 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Express LocalDB 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書主題。

總而言之，LocalDB 可讓您：

-   使用 **sqllocaldb.exe i** 來探索預設執行個體的名稱。

-   使用 **AttachDBFilename** 連接字串關鍵字來指定伺服器應該附加的資料庫檔案。 使用 **AttachDBFilename** 時，如果您沒有使用 **Database** 連接字串關鍵字來指定資料庫的名稱，系統就會在應用程式關閉時從 LocalDB 執行個體中移除資料庫。

-   請在連接字串中指定 LocalDB 執行個體。 例如，以下是範例 SQLSRV 連接字串：

    ```php
    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array( 'Database'=>'myData'));

    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array('AttachDBFileName'=>'c:\\myData.MDF','Database'=>'myData'));

    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array('AttachDBFileName'=>'c:\\myData.MDF'));
    ```

    接下來是 PDO_SQLSRV 連接字串的範例：  

    ```php
    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'Database=myData', NULL, NULL);

    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'AttachDBFileName=c:\\myData.MDF;Database=myData ',
        NULL, NULL);

    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'AttachDBFileName=c:\\myData.MDF', NULL, NULL);  
    ```

必要時，您可以使用 sqllocaldb.exe 來建立 LocalDB 執行個體。 您也可以使用 sqlcmd.exe，在 LocalDB 執行個體中加入和修改資料庫。 例如： `sqlcmd -S (localdb)\v11.0` 。 (在 IIS 中執行時，您必須在正確的帳戶下執行，以取得與您在命令列執行時相同的結果；如需詳細資訊，請參閱[搭配完整 IIS 使用 LocalDB，第 2 部分：執行個體擁有權](/archive/blogs/sqlexpress/using-localdb-with-full-iis-part-2-instance-ownership)) \(英文\)。

以下是使用 SQLSRV 驅動程式的範例連接字串，其會連線至名為 myInstance 的 LocalDB 具名執行個體中的資料庫：

```php
$conn = sqlsrv_connect( '(localdb)\\myInstance',
    array( 'Database'=>'myData'));
```

以下是使用 PDO_SQLSRV 驅動程式的範例連接字串，其會連線至名為 myInstance 的 LocalDB 具名執行個體中的資料庫：  
  
```php
$conn = new PDO( 'sqlsrv:server=(localdb)\\myInstance;'
    . 'database=myData', NULL, NULL);
```

如需有關安裝 LocalDB 的指示，請參閱 [LocalDB 文件](../../database-engine/configure-windows/sql-server-express-localdb.md)。 如果您使用 sqlcmd.exe 來修改 LocalDB 執行個體中的資料，您將需要 [sqlcmd 公用程式](../../tools/sqlcmd-utility.md)。

## <a name="see-also"></a>另請參閱

[連線到伺服器](../../connect/php/connecting-to-the-server.md)