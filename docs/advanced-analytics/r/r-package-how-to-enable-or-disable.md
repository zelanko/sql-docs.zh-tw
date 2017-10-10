---
title: "啟用或停用 SQL Server 的 R 封裝管理 |Microsoft 文件"
ms.custom: 
ms.date: 10/05/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6e384893-04da-43f9-b100-bfe99888f085
caps.latest.revision: 7
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 29122bdf543e82c1f429cf401b5fe1d8383515fc
ms.openlocfilehash: 88337da76b3a44b9dc797fd1d9f187bfda7396c8
ms.contentlocale: zh-tw
ms.lasthandoff: 10/10/2017

---
# <a name="enable-or-disable-r-package-management-for-sql-server"></a>啟用或停用 SQL Server 的 R 封裝管理

本文描述啟用或停用 SQL Server 2017 中新的封裝管理功能的程序。 這項功能可讓資料庫管理員來控制執行個體上的套件安裝。 功能必須依賴新的資料庫角色，以授與使用者的能力安裝所需的 R 封裝，或與其他使用者共用封裝。

根據預設，SQL Server 的外部封裝管理功能已停用，即使已安裝的機器學習功能。

若要[啟用](#bkmk_enable)此功能是兩個步驟的程序，並需要相關協助資料庫管理員：

1.  在 SQL Server 執行個體上啟用封裝管理 (每個 SQL Server 執行個體一次)

2.  在 SQL 資料庫上啟用封裝管理 (每個 SQL Server 資料庫一次)

若要[停用](#bkmk_disable)的封裝管理功能，反轉移除資料庫層級的套件和權限的程序，然後從伺服器移除角色：

1.  在每個資料庫上停用封裝管理 (每個資料庫一次)

2.  在 SQL Server 執行個體上停用封裝管理 (每個執行個體一次)

## <a name="bkmk_enable"></a>啟用封裝管理

若要啟用或停用封裝管理需要命令列公用程式**RegisterRExt.exe**，隨附於**RevoScaleR**封裝。

1. 開啟提升權限的命令提示字元並瀏覽至包含 RegisterRExt.exe 公用程式的資料夾。 預設位置是`<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExe.exe`。

2. 執行下列命令，並提供您的環境適當引數：

    `RegisterRExt.exe /installpkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    此命令會建立所需的封裝管理 SQL Server 電腦上的執行個體層級物件。 它也會執行個體的 [啟動列] 重新啟動。

    如果您未指定執行個體，則會使用預設執行個體。

    如果您未指定使用者，則會使用目前的安全性內容。

2.  若要加入封裝管理資料庫層級，請從提升權限的命令提示字元執行下列命令：

    `RegisterRExt.exe /installpkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`
   
    此命令會建立一些資料庫成品，包括下列用來控制使用者權限的資料庫角色： `rpkgs-users`， `rpkgs-private`，和`rpkgs-shared`。

    如果您未指定使用者，則會使用目前的安全性內容。

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

4.  任何具有適當的權限的使用者尚未啟用的功能之後，可以使用[建立外部程式庫](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)T-SQL 加入封裝中的陳述式。 如需其運作方式的範例，請參閱[SQL Server 上安裝其他封裝](install-additional-r-packages-on-sql-server.md)。

## <a name="bkmk_disable"></a>停用封裝管理

1.  從提升權限的命令提示字元，執行下列命令以停用資料庫層級的封裝管理：

    `RegisterRExt.exe /uninstallpkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`

    用以管理封裝的情況下執行此命令一次針對每個資料庫。 此命令會移除封裝管理從指定的資料庫相關的資料庫物件。 它也會移除已安裝 SQL Server 電腦上的受保護的檔案系統位置中的所有封裝。

2.  （選擇性）已清除所有資料庫的封裝使用上述步驟之後，請從提升權限的命令提示字元執行下列命令：

    `RegisterRExt.exe /uninstallpkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    此命令會從執行個體移除封裝管理功能。

## <a name="see-also"></a>另請參閱

[SQL Server 的 R 封裝管理](r-package-management-for-sql-server-r-services.md)
