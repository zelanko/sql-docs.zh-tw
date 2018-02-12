---
title: "啟用或停用 SQL Server 的 R 封裝管理 |Microsoft 文件"
ms.custom: 
ms.date: 01/04/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6e384893-04da-43f9-b100-bfe99888f085
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 35bcae1e29e9b640d2e04b9adc788e382b18b6e8
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2018
---
# <a name="enable-or-disable-r-package-management-for-sql-server"></a>啟用或停用 SQL Server 的 R 封裝管理
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文描述 SQL Server 2017，設計可讓資料庫管理員來控制使用 T-SQL，而不是。 執行個體上的套件安裝的新封裝管理功能

要封裝管理 frature 已啟用，您也可以使用 R 命令上資料庫的方式遠端用戶端安裝封裝。

> [!NOTE]
> 根據預設，SQL Server 的外部封裝管理功能已停用，即使已安裝的機器學習功能。 

## <a name="enable-package-management"></a>啟用封裝管理

若要[啟用](#bkmk_enable)這項功能是兩個步驟的程序，需要資料庫管理員：

1.  在 SQL Server 執行個體上啟用封裝管理 (每個 SQL Server 執行個體一次)

2.  在 SQL 資料庫上啟用封裝管理 (每個 SQL Server 資料庫一次)

若要[停用](#bkmk_disable)的封裝管理功能，反轉移除資料庫層級的套件和權限的程序，然後從伺服器移除角色：

1.  在每個資料庫上停用封裝管理 (每個資料庫一次)

2.  在 SQL Server 執行個體上停用封裝管理 (每個執行個體一次)

## <a name="bkmk_enable"></a>啟用封裝管理

若要啟用或停用封裝管理，使用命令列公用程式**RegisterRExt.exe**，隨附於**RevoScaleR**封裝。

1. 開啟提升權限的命令提示字元並瀏覽至包含 RegisterRExt.exe 公用程式的資料夾。 預設位置是`<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExe.exe`。

2. 執行下列命令，並提供適當的引數為您的環境：

    `RegisterRExt.exe /installpkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    此命令會建立所需的封裝管理 SQL Server 電腦上的執行個體層級物件。 它也會執行個體的 [啟動列] 重新啟動。

    如果您未指定執行個體，則會使用預設執行個體。 如果您未指定使用者，則會使用目前的安全性內容。 例如，下列命令會啟用 RegisterRExt.exe，使用的認證開啟命令提示字元中的使用者路徑中的執行個體上的封裝管理：

    `REgisterRExt.exe /installpkgmgmt`

2.  若要加入封裝管理特定資料庫，請從提升權限的命令提示字元執行下列命令：

    `RegisterRExt.exe /installpkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`
   
    此命令會建立一些資料庫成品，包括下列用來控制使用者權限的資料庫角色： `rpkgs-users`， `rpkgs-private`，和`rpkgs-shared`。

    例如，下列命令會啟用在資料庫上，執行 RegisterRExt 的執行個體上的封裝管理。 如果您未指定使用者，則會使用目前的安全性內容。 

    `RegisterRExt.exe /installpkgmgmt /database:TestDB`

3. 每個資料庫必須已安裝封裝中重複命令。

4.  若要確認已成功建立新的角色，在 SQL Server Management Studio 中，按一下資料庫，展開 **安全性**，然後展開**資料庫角色**。

    您也可以執行的查詢上 sys.database_principals 如下所示：

    ```SQL
    SELECT pr.principal_id, pr.name, pr.type_desc,   
        pr.authentication_type_desc, pe.state_desc,   
        pe.permission_name, s.name + '.' + o.name AS ObjectName  
    FROM sys.database_principals AS pr  
    JOIN sys.database_permissions AS pe  
        ON pe.grantee_principal_id = pr.principal_id  
    JOIN sys.objects AS o  
        ON pe.major_id = o.object_id  
    JOIN sys.schemas AS s  
        ON o.schema_id = s.schema_id;
    ```

4.  尚未啟用的功能之後，您可以連線到伺服器並安裝或同步處理封裝遠端電腦上，使用 R 命令。 如需其運作方式的範例，請參閱[SQL Server 上安裝其他封裝](install-additional-r-packages-on-sql-server.md)。

## <a name="bkmk_disable"></a>停用封裝管理

1.  從提升權限的命令提示字元，RegisterRExt 公用程式再次執行，並停用套件管理資料庫層級：

    `RegisterRExt.exe /uninstallpkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`

    此命令會移除封裝管理從指定的資料庫相關的資料庫物件。 它也會移除已安裝 SQL Server 電腦上的受保護的檔案系統位置中的所有封裝。

2. 用以管理封裝的情況下執行此命令一次針對每個資料庫。 

3.  （選擇性）已清除所有資料庫的封裝使用上述步驟之後，請從提升權限的命令提示字元執行下列命令：

    `RegisterRExt.exe /uninstallpkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    此命令會從執行個體移除封裝管理功能。 您可能需要手動重新啟動 Launchpad 服務一次才能看到變更。

## <a name="see-also"></a>另請參閱

[SQL Server 的 R 套件管理](r-package-management-for-sql-server-r-services.md)
