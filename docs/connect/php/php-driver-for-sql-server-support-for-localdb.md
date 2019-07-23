---
title: LocalDB 的支援 |Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d315ad6a-0d50-4093-80c2-2f11217237c2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f6da7f1aed956c8b2f5c71496c9c121f6006eabb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67935952"
---
# <a name="support-for-localdb"></a>LocalDB 的支援

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

LocalDB 是的輕量版本[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , 已于之後[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]提供。 本主題將討論如何連接到 LocalDB 執行個體中的資料庫。

## <a name="remarks"></a>Remarks

如需 LocalDB 的詳細資訊, 包括如何安裝 localdb 和設定 localdb 實例, 請參閱快速[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] LocalDB 上[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]的《線上叢書》主題。

簡單地說, LocalDB 可讓您:

-   使用**sqllocaldb**探索預設實例的名稱。

-   使用 **AttachDBFilename** 連接字串關鍵字來指定伺服器應該附加的資料庫檔案。 使用 **AttachDBFilename** 時，如果您沒有使用 **Database** 連接字串關鍵字來指定資料庫的名稱，系統就會在應用程式關閉時從 LocalDB 執行個體中移除資料庫。

-   請在連接字串中指定 LocalDB 執行個體。 例如, 以下是範例 SQLSRV 連接字串:

    ```php
    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array( 'Database'=>'myData'));

    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array('AttachDBFileName'=>'c:\\myData.MDF','Database'=>'myData'));

    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array('AttachDBFileName'=>'c:\\myData.MDF'));
    ```

    接下來是範例 PDO_SQLSRV 連接字串:  

    ```php
    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'Database=myData', NULL, NULL);

    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'AttachDBFileName=c:\\myData.MDF;Database=myData ',
        NULL, NULL);

    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'AttachDBFileName=c:\\myData.MDF', NULL, NULL);  
    ```

必要時，您可以使用 sqllocaldb.exe 來建立 LocalDB 執行個體。 您也可以使用 sqlcmd.exe，在 LocalDB 執行個體中加入和修改資料庫。 例如， `sqlcmd -S (localdb)\v11.0`。 (在 IIS 中執行時, 您必須在正確的帳戶下執行, 以取得與您在命令列執行時相同的結果; 如需詳細資訊, 請參閱[使用 LocalDB 搭配完整的 IIS, 第2部分: 實例擁有權](https://blogs.msdn.com/b/sqlexpress/archive/2011/12/09/using-localdb-with-full-iis-part-2-instance-ownership.aspx))。

以下是使用 SQLSRV 驅動程式的範例連接字串, 其會連接到名為 myInstance 的 LocalDB 實例中的資料庫:

```php
$conn = sqlsrv_connect( '(localdb)\\myInstance',
    array( 'Database'=>'myData'));
```

以下是使用 PDO_SQLSRV 驅動程式的範例連接字串, 它會連接到名為 myInstance 的 LocalDB 實例中的資料庫:  
  
```php
$conn = new PDO( 'sqlsrv:server=(localdb)\\myInstance;'
    . 'database=myData', NULL, NULL);
```

如需安裝 LocalDB 的指示, 請參閱[LocalDB 檔](../../database-engine/configure-windows/sql-server-2016-express-localdb.md)。 如果您使用 sqlcmd 來修改 LocalDB 實例中的資料, 您將需要[sqlcmd 公用程式](../../tools/sqlcmd-utility.md)。

## <a name="see-also"></a>另請參閱

[連線到伺服器](../../connect/php/connecting-to-the-server.md)
