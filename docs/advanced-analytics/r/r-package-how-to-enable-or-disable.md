---
title: 啟用或停用遠端的 R 封裝管理-SQL Server Machine Learning 服務
description: 啟用 SQL Server 2016 R Services 或 SQL Server 2017 Machine Learning 服務 （資料庫） 上的遠端 R 封裝管理
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/10/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: ee52fd9b7a116156f794303b828a83e9b06de6ab
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62641815"
---
# <a name="enable-or-disable-remote-package-management-for-sql-server"></a>啟用或停用 SQL Server 的遠端封裝管理
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文說明如何啟用遠端管理用戶端工作站或不同的 Machine Learning Server 的 R 套件。 SQL Server 上啟用封裝管理功能之後，您可以在用戶端上使用 RevoScaleR 命令，SQL Server 上安裝封裝項目。

> [!NOTE]
> 目前支援的 R 程式庫管理;已在規劃中的 Python 支援。

根據預設，適用於 SQL Server 外部的封裝管理功能已停用。 您必須執行個別的指令碼，以啟用功能，在下一節中所述。

## <a name="overview-of-process-and-tools"></a>處理程序和工具的概觀

若要啟用或停用封裝管理 SQL Server 上的，使用命令列公用程式**RegisterRExt.exe**，這是隨附**RevoScaleR**封裝。

[啟用](#bkmk_enable)這項功能是兩個步驟的程序，需要資料庫管理員： 您的 SQL Server 執行個體 （每個 SQL Server 執行個體） 上啟用封裝管理，然後啟用 SQL database （每個 SQL Server 上的套件管理資料庫）。

[停用](#bkmk_disable)封裝管理功能也需要 multipel 步驟： 您移除資料庫層級封裝和權限 （每個資料庫），並從 （每個執行個體） 伺服器移除角色。

## <a name="bkmk_enable"></a> 啟用封裝管理

1. SQL Server 上，開啟提升權限的命令提示字元並瀏覽至包含此公用程式，RegisterRExt.exe 的資料夾。 預設位置是`<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExe.exe`。

2. 執行下列命令，並提供適當的引數，為您的環境：

    `RegisterRExt.exe /install pkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    此命令會建立執行個體層級物件，封裝管理所需的 SQL Server 電腦上。 它也會執行個體的 [啟動列] 重新啟動。

    如果您未指定執行個體，則會使用預設執行個體。 如果您未指定使用者，則會使用目前的安全性內容。 例如，下列命令會啟用在 RegisterRExt.exe，使用的認證開啟命令提示字元中的使用者路徑中的執行個體上的套件管理：

    `REgisterRExt.exe /install pkgmgmt`

3. 若要加入特定的資料庫中的套件管理，請從提升權限的命令提示字元執行下列命令：

    `RegisterRExt.exe /install pkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`
   
    此命令會建立一些資料庫成品，包括下列用來控制使用者權限的資料庫角色： `rpkgs-users`， `rpkgs-private`，和`rpkgs-shared`。

    例如，下列命令會啟用 RegisterRExt 執行所在的執行個體上的資料庫上的套件管理。 如果您未指定使用者，則會使用目前的安全性內容。

    `RegisterRExt.exe /install pkgmgmt /database:TestDB`

4. 針對每個套件必須安裝所在的資料庫，重複執行命令。

5. 若要確認已成功建立新的角色，在 SQL Server Management Studio 中，按一下資料庫，展開**安全性**，展開**資料庫角色**。

    您也可以執行查詢上 sys.database_principals 如下所示：

    ```sql
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

您已啟用這項功能之後，您可以使用 RevoScaleR 函式，來安裝或從遠端 R 用戶端解除安裝套件。

## <a name="bkmk_disable"></a> 停用封裝管理

1. 從提升權限的命令提示字元中，RegisterRExt 公用程式再次執行，並停用資料庫層級的封裝管理：

    `RegisterRExt.exe /uninstall pkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`

    此命令會從指定的資料庫與封裝管理相關的資料庫物件。 它也會移除安裝從受保護的檔案系統位置，SQL Server 電腦上的所有套件。

2. 重複此命令使用封裝管理每個資料庫上。

3.  （選擇性）已清除所有資料庫的套件使用上述步驟之後，請從提升權限的命令提示字元執行下列命令：

    `RegisterRExt.exe /uninstall pkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    此命令會從執行個體移除封裝管理功能。 您可能需要手動重新啟動 Launchpad 服務一次，才能看到變更。

## <a name="next-steps"></a>後續步驟

+ [使用 RevoScaleR 安裝新的 R 套件](use-revoscaler-to-manage-r-packages.md)
+ [安裝 R 套件的秘訣](packages-installed-in-user-libraries.md)
+ [預設封裝](installing-and-managing-r-packages.md)
