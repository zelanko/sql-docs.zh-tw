---
title: LocalDB 的支援 | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d315ad6a-0d50-4093-80c2-2f11217237c2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7d31758d437ad8b175fca86bd5e25b0aff2c9989
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80909134"
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

必要時，您可以使用 sqllocaldb.exe 來建立 LocalDB 執行個體。 您也可以使用 sqlcmd.exe，在 LocalDB 執行個體中加入和修改資料庫。 例如： `sqlcmd -S (localdb)\v11.0` 。 (在 IIS 中執行時，您必須在正確的帳戶下執行，以取得與您在命令列執行時相同的結果；如需詳細資訊，請參閱[搭配完整 IIS 使用 LocalDB，第 2 部分：執行個體擁有權](https://blogs.msdn.com/b/sqlexpress/archive/2011/12/09/using-localdb-with-full-iis-part-2-instance-ownership.aspx)) \(英文\)。

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

如需有關安裝 LocalDB 的指示，請參閱 [LocalDB 文件](../../database-engine/configure-windows/sql-server-2016-express-localdb.md)。 如果您使用 sqlcmd.exe 來修改 LocalDB 執行個體中的資料，您將需要 [sqlcmd 公用程式](../../tools/sqlcmd-utility.md)。

## <a name="see-also"></a>另請參閱

[連線到伺服器](../../connect/php/connecting-to-the-server.md)
