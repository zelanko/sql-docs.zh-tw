
---
title: "PHP Driver for SQL Server Support for LocalDB |Microsoft 文件"
ms.custom: 
ms.date: 02/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d315ad6a-0d50-4093-80c2-2f11217237c2
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a54071c75ca4437974be7b742ee3285972850e0a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="php-driver-for-sql-server-support-for-localdb"></a>PHP Driver for SQL Server Support for LocalDB (PHP Driver for SQL Server 對 LocalDB 的支援)

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

從開始[!INCLUDE[ssSQL11](../../includes/sssql11_md.md)]，輕量版[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]名為 LocalDB，將可使用。 本主題將討論如何連接到 LocalDB 執行個體中的資料庫。

## <a name="remarks"></a>備註

如需有關 LocalDB，包括如何安裝 LocalDB 和設定 LocalDB 執行個體，請參閱[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]上的線上叢書 》 主題[!INCLUDE[ssSQL11](../../includes/sssql11_md.md)]Express LocalDB。

總而言之，LocalDB 可讓您：

-   使用**sqllocaldb.exe 我**探索預設執行個體的名稱。

-   使用**AttachDBFilename**應該附加至指定的資料庫檔案伺服器的連接字串關鍵字。 使用時**AttachDBFilename**，如果您未指定的資料庫名稱**資料庫**連接字串關鍵字，資料庫會移除的 LocalDB 執行個體時應用程式會關閉。

-   在連接字串中指定的 LocalDB 執行個體。 例如，以下是範例 SQLSRV 連接字串：

    ```php
    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array( 'Database'=>'myData'));

    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array('AttachDBFileName'=>'c:\\myData.MDF','Database'=>'myData'));

    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array('AttachDBFileName'=>'c:\\myData.MDF'));
    ```

    接下來是範例 PDO_SQLSRV 連接字串：  

    ```php
    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'Database=myData', NULL, NULL);

    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'AttachDBFileName=c:\\myData.MDF;Database=myData ',
        NULL, NULL);

    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'AttachDBFileName=c:\\myData.MDF', NULL, NULL);  
    ```

必要時，您可以使用 sqllocaldb.exe 來建立 LocalDB 執行個體。 您也可以使用 sqlcmd.exe，在 LocalDB 執行個體中加入和修改資料庫。 例如， `sqlcmd -S (localdb)\v11.0`。 (在 IIS 執行時，您需要執行以取得當您執行在命令列; 相同的結果正確的帳戶查看[使用 LocalDB 使用完整 IIS 時，第 2 部分： 執行個體擁有權](http://blogs.msdn.com/b/sqlexpress/archive/2011/12/09/using-localdb-with-full-iis-part-2-instance-ownership.aspx)如需詳細資訊。)

以下是範例連接字串使用 SQLSRV 驅動程式連接到 LocalDB，名為名為 myInstance 的執行個體中的資料庫：

```php
$conn = sqlsrv_connect( '(localdb)\\myInstance',
    array( 'Database'=>'myData'));
```

以下是範例連接字串使用 PDO_SQLSRV 驅動程式連接到 LocalDB，名為名為 myInstance 的執行個體中的資料庫：  
  
```php
$conn = new PDO( 'sqlsrv:server=(localdb)\\myInstance;'
    . 'database=myData', NULL, NULL);
```

您可以下載從 LocalDB [SQL Server 2012 功能套件頁面](http://go.microsoft.com/fwlink/?LinkID=236805)，或從[!INCLUDE[ssSQL11](../../includes/sssql11_md.md)]Express edition。 如果您將使用 sqlcmd.exe 來修改 LocalDB 執行個體中的資料，您必須從 sqlcmd [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)]，您可以從命令列公用程式下載中取得[!INCLUDE[ssSQL11](../../includes/sssql11_md.md)]功能套件頁面。

## <a name="see-also"></a>另請參閱

[連接到伺服器](../../connect/php/connecting-to-the-server.md)

