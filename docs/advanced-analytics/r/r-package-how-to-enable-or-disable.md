---
title: 啟用或停用遠端 SQL Server 機器學習的 R 封裝管理 |Microsoft 文件
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: fc51428a4e6bd214fee8c4889eb218f3664ba118
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="enable-or-disable-remote-package-management-for-sql-server"></a>啟用或停用的 SQL Server 的遠端封裝管理
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文說明如何啟用 R 封裝，從遠端機器學習的伺服器執行個體的管理。 封裝管理功能已啟用之後，您可以使用 RevoScaleR 命令，將資料庫從遠端用戶端上安裝封裝。

> [!NOTE]
> 目前支援的 R 程式庫管理;正在規劃 Python 的支援。

根據預設，SQL Server 的外部封裝管理功能已停用，即使已安裝的機器學習功能。 您必須執行個別的指令碼，以啟用功能下, 一節中所述。

## <a name="overview-of-process-and-tools"></a>處理程序和工具的概觀

若要啟用或停用封裝管理，使用命令列公用程式**RegisterRExt.exe**，隨附於**RevoScaleR**封裝。

[啟用](#bkmk_enable)這項功能是兩個步驟的程序，需要資料庫管理員： 在封裝上啟用管理 SQL Server 執行個體 （每個 SQL Server 執行個體），然後再啟用 SQL database （每個 SQL Server 上的封裝管理資料庫）。

[停用](#bkmk_disable)封裝管理功能也需要 multipel 步驟執行： 您移除資料庫層級的套件和權限 （每個資料庫），並從 （每個執行個體） 伺服器移除角色。

## <a name="bkmk_enable"></a> 啟用封裝管理

1. 開啟提升權限的命令提示字元並瀏覽至包含 RegisterRExt.exe 公用程式的資料夾。 預設位置是`<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExe.exe`。

2. 執行下列命令，並提供適當的引數為您的環境：

    `RegisterRExt.exe /installpkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    此命令會建立所需的封裝管理 SQL Server 電腦上的執行個體層級物件。 它也會執行個體的 [啟動列] 重新啟動。

    如果您未指定執行個體，則會使用預設執行個體。 如果您未指定使用者，則會使用目前的安全性內容。 例如，下列命令會啟用 RegisterRExt.exe，使用的認證開啟命令提示字元中的使用者路徑中的執行個體上的封裝管理：

    `REgisterRExt.exe /installpkgmgmt`

3. 若要加入封裝管理特定資料庫，請從提升權限的命令提示字元執行下列命令：

    `RegisterRExt.exe /installpkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`
   
    此命令會建立一些資料庫成品，包括下列用來控制使用者權限的資料庫角色： `rpkgs-users`， `rpkgs-private`，和`rpkgs-shared`。

    例如，下列命令會啟用在資料庫上，執行 RegisterRExt 的執行個體上的封裝管理。 如果您未指定使用者，則會使用目前的安全性內容。

    `RegisterRExt.exe /installpkgmgmt /database:TestDB`

4. 每個資料庫必須已安裝封裝中重複命令。

5. 若要確認已成功建立新的角色，在 SQL Server Management Studio 中，按一下資料庫，展開 **安全性**，然後展開**資料庫角色**。

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

啟用此功能之後，您可以安裝或解除安裝封裝，從遠端 R 用戶端使用 RevoScaleR 函式。

## <a name="bkmk_disable"></a> 停用封裝管理

1. 從提升權限的命令提示字元，RegisterRExt 公用程式再次執行，並停用套件管理資料庫層級：

    `RegisterRExt.exe /uninstallpkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`

    此命令會移除封裝管理從指定的資料庫相關的資料庫物件。 它也會移除已安裝 SQL Server 電腦上的受保護的檔案系統位置中的所有封裝。

2. 重複此命令，用以封裝管理每個資料庫上。

3.  （選擇性）已清除所有資料庫的封裝使用上述步驟之後，請從提升權限的命令提示字元執行下列命令：

    `RegisterRExt.exe /uninstallpkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    此命令會從執行個體移除封裝管理功能。 您可能需要手動重新啟動 Launchpad 服務一次才能看到變更。

