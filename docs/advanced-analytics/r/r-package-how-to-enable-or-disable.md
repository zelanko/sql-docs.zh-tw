---
title: 啟用或停用遠端 R 套件管理
description: 在 SQL Server 2016 R Services 或 SQL Server Machine Learning 服務上啟用遠端 R 封裝管理 (資料庫內)
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 260109e978c8997622f24c41341e11f1e2efa7cc
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715637"
---
# <a name="enable-or-disable-remote-package-management-for-sql-server"></a>啟用或停用 SQL Server 的遠端套件管理
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文說明如何從用戶端工作站或不同的 Machine Learning Server 啟用 R 封裝的遠端系統管理。 在 SQL Server 上啟用封裝管理功能之後, 您可以在用戶端上使用 RevoScaleR 命令, 將套件安裝在 SQL Server 上。

> [!NOTE]
> 目前支援 R 程式庫的管理;Python 的支援已在藍圖中。

根據預設, SQL Server 的外部封裝管理功能已停用。 您必須執行個別的腳本來啟用此功能, 如下一節所述。

## <a name="overview-of-process-and-tools"></a>進程和工具的總覽

若要啟用或停用 SQL Server 上的套件管理, 請使用**RevoScaleR**套件隨附的命令列公用程式**registerrext.exe。**

[啟用](#bkmk_enable)這項功能是兩個步驟的程式, 需要資料庫管理員: 您會在 SQL Server 實例上啟用封裝管理 (每個 SQL Server 實例一次), 然後在 SQL 資料庫上啟用封裝管理 (每個 SQL Server 資料庫一次)。).

[停](#bkmk_disable)用封裝管理功能也需要 multipel 步驟: 您會移除資料庫層級封裝和許可權 (每個資料庫一次), 然後從伺服器移除角色 (每個實例一次)。

## <a name="bkmk_enable"></a>啟用套件管理

1. 在 SQL Server 上, 開啟提升許可權的命令提示字元, 並流覽至包含公用程式 Registerrext.exe 的資料夾。 預設位置是`<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExe.exe`。

2. 執行下列命令, 為您的環境提供適當的引數:

    `RegisterRExt.exe /install pkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    此命令會在 SQL Server 電腦上建立套件管理所需的實例層級物件。 它也會重新開機實例的啟動列。

    如果您未指定實例, 則會使用預設實例。 如果您未指定使用者, 則會使用目前的安全性內容。 例如, 下列命令會使用開啟命令提示字元的使用者認證, 在 Registerrext.exe 路徑中的實例上啟用套件管理:

    `REgisterRExt.exe /install pkgmgmt`

3. 若要將套件管理新增至特定的資料庫, 請從提高許可權的命令提示字元執行下列命令:

    `RegisterRExt.exe /install pkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`
   
    此命令會建立一些資料庫成品, 包括用來控制使用者權限的下列資料庫角色: `rpkgs-users`、 `rpkgs-private`和`rpkgs-shared`。

    例如, 下列命令會在執行 Registerrext.exe 的實例上啟用資料庫上的封裝管理。 如果您未指定使用者, 則會使用目前的安全性內容。

    `RegisterRExt.exe /install pkgmgmt /database:TestDB`

4. 針對必須安裝套件的每個資料庫重複此命令。

5. 若要確認已成功建立新角色, 請在 SQL Server Management Studio 中, 按一下資料庫, 展開 **安全性**, 然後展開 **資料庫角色**。

    您也可以在 database_principals 上執行查詢, 如下所示:

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

啟用這項功能之後, 您可以使用 RevoScaleR 函式, 從遠端 R 用戶端安裝或卸載封裝。

## <a name="bkmk_disable"></a>停用套件管理

1. 從提高許可權的命令提示字元, 再次執行 Registerrext.exe 公用程式, 並在資料庫層級停用封裝管理:

    `RegisterRExt.exe /uninstall pkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`

    此命令會從指定的資料庫中移除與封裝管理相關的資料庫物件。 它也會移除從 SQL Server 電腦上受保護的檔案系統位置安裝的所有封裝。

2. 在使用套件管理的每個資料庫上重複此命令。

3.  選擇性使用上述步驟清除封裝的所有資料庫之後, 請從提升許可權的命令提示字元執行下列命令:

    `RegisterRExt.exe /uninstall pkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    此命令會從實例移除封裝管理功能。 您可能需要手動重新開機啟動列服務, 以查看變更。

## <a name="next-steps"></a>後續步驟

+ [使用 RevoScaleR 來安裝新的 R 套件](use-revoscaler-to-manage-r-packages.md)
+ [安裝 R 套件的秘訣](packages-installed-in-user-libraries.md)
+ [預設封裝](../package-management/default-packages.md)
