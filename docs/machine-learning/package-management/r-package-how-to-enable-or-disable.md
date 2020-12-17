---
title: 啟用或停用遠端 R 套件管理
description: 在 SQL Server 2016 R Services 或 SQL Server Machine Learning Services 上啟用遠端 R 套件管理 (資料庫內)
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 06/13/2019
ms.topic: how-to
author: garyericson
ms.author: garye
monikerRange: =sql-server-2016||=sql-server-2017
ms.openlocfilehash: c425d2c544069f19414e6731cdcd1f9290f07f36
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97470969"
---
# <a name="enable-or-disable-remote-package-management-for-sql-server"></a>啟用或停用 SQL Server 的遠端套件管理
[!INCLUDE [SQL Server 2016 and 2017 only](../../includes/applies-to-version/sqlserver2016-2017-only.md)]

此文章說明如何從用戶端工作站或不同的 Machine Learning Server 啟用 R 套件的遠端管理。 在 SQL Server 上啟用套件管理功能之後，就可以在用戶端上使用 RevoScaleR 命令將套件安裝在 SQL Server 上。

SQL Server 的外部套件管理功能預設為停用。 您必須執行個別指令碼來啟用此功能，如下一節所述。

## <a name="overview-of-process-and-tools"></a>程序與工具概觀

若要在 SQL Server 上啟用或停用套件管理，請使用 **RevoScaleR** 套件中隨附的命令列公用程式 **RegisterRExt.exe**。

[啟用](#bkmk_enable)此功能是兩步驟程序，而且需由資料庫管理員執行：您必須在 SQL Server 執行個體上啟用套件管理 (每個 SQL Server 執行個體個別啟用)，然後在 SQL 資料庫上啟用套件管理 (每個 SQL Server 資料庫個別啟用)。

[停用](#bkmk_disable)套件管理功能也需要多個步驟：您必須移除資料庫層級套件與權限 (每個資料庫個別移除)，然後從伺服器移除角色 (每個執行個體個別移除)。

## <a name="enable-package-management"></a><a name="bkmk_enable"></a> 啟用套件管理

1. 在 SQL Server 上，開啟提升權限的命令提示字元，並瀏覽至包含公用程式 RegisterRExt.exe 的資料夾。 預設位置為 `<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExe.exe`。

2. 執行下列命令，並為您的環境提供適當的引數：

    `RegisterRExt.exe /install pkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    此命令會在 SQL Server 電腦上建立套件管理所需的執行個體層級物件， 此命令也會重新啟動執行個體的 Launchpad。

    如果您未指定執行個體，系統會使用預設的執行個體。 如果您未指定使用者，系統會使用目前的資訊安全內容。 例如，下列命令會使用開啟命令提示字元的使用者認證，對預設的執行個體啟用套件管理：

    `REgisterRExt.exe /install pkgmgmt`

3. 若要將套件管理新增至特定資料庫，請從提高權限的命令提示字元執行下列命令：

    `RegisterRExt.exe /install pkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`
   
    此命令會建立一些資料庫成品，包括下列用來控制使用者權限的資料庫角色：`rpkgs-users`、`rpkgs-private` 與 `rpkgs-shared`。

    例如，下列命令會對預設執行個體的資料庫啟用套件管理。 如果您未指定使用者，系統會使用目前的資訊安全內容。

    `RegisterRExt.exe /install pkgmgmt /database:TestDB`

4. 請為必須安裝套件的每個資料庫重複執行此命令。

5. 若要確認已成功建立新角色，請在 SQL Server Management Studio 中，按一下資料庫、展開 [安全性]  ，然後展開 [資料庫角色]  。

    您也可以如下所示，在 sys.database_principals 上執行查詢：

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

啟用此功能之後，您就可以使用 RevoScaleR 函式，從遠端 R 用戶端安裝或解除安裝套件。

## <a name="disable-package-management"></a><a name="bkmk_disable"></a> 停用套件管理

1. 再次從提升權限的命令提示字元執行 RegisterRExt 公用程式，並在資料庫層級停用套件管理：

    `RegisterRExt.exe /uninstall pkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`

    此命令會從指定的資料庫移除與套件管理有關的資料庫物件， 此命令也會從 SQL Server 電腦上受保護的檔案系統位置，移除已安裝的所有套件。

2. 請在使用套件管理的每個資料庫上重複執行此命令。

3.  (選擇性) 使用前述步驟清除所有資料庫的套件之後，從提高權限的命令提示字元執行下列命令：

    `RegisterRExt.exe /uninstall pkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    此命令會從執行個體移除套件管理功能。 您可能需要再次手動重新啟動 Launchpad 服務，以查看變更。

## <a name="next-steps"></a>後續步驟

+ [使用 RevoScaleR 來安裝 R 套件](install-r-packages-with-revoscaler.md)
+ [取得 R 套件資訊](r-package-information.md)
+ [使用 R 套件的祕訣](tips-for-using-r-packages.md)
