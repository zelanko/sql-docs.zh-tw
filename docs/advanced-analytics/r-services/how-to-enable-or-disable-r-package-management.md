---
title: "如何啟用或停用 R 封裝管理 | Microsoft Docs"
ms.custom: ""
ms.date: "12/22/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6e384893-04da-43f9-b100-bfe99888f085
caps.latest.revision: 7
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# 如何啟用或停用 R 封裝管理

SQL Server 執行個體上預設會停用封裝管理，即使已安裝 R Services 亦然。 啟用這項功能是兩個步驟的程序，必須由資料庫管理員執行： 

1. 在 SQL Server 執行個體上啟用封裝管理 (每個 SQL Server 執行個體一次) 
2. 在 SQL 資料庫上啟用封裝管理 (每個 SQL Server 資料庫一次) 


停用封裝管理功能時，請反轉程序以移除資料庫層級封裝和權限，然後從伺服器移除角色：
 
1. 在每個資料庫上停用封裝管理 (每個資料庫一次) 
2. 在 SQL Server 執行個體上停用封裝管理 (每個執行個體一次) 

> [!IMPORTANT]
> 這項功能仍在開發中。 請注意，此語法或功能可能會在未來版本中變更。 

### <a name="to-enable-package-management"></a>啟用封裝管理

啟用或停用封裝管理套件需要命令列公用程式 **RegisterRExt.exe**，該公用程式隨附於與 SQL Server R 服務一起安裝的 **RevoScaleR** 封裝中。 預設位置為：

`<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExe.exe` 
    
1. 開啟提升權限的命令提示字元並使用下列命令：

    `RegisterRExt.exe /installpkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    此命令會在 SQL Server 電腦上，建立封裝管理所需的執行個體層級成品。 

2. 若要在資料庫層級加入封裝管理，請針對必須安裝封裝的每個資料庫，從提升權限的命令提示字元執行下列命令： 

    `RegisterRExt.exe /installpkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]` 

    此命令會建立一些資料庫成品，包括控制使用者權限所需的下列資料庫角色︰**rpkgs-users**、**rpkgs-private** 和 **rpkgs-shared** 

### <a name="to-disable-package-management"></a>停用封裝管理 

1. 從提升權限的命令提示字元，執行下列命令以停用資料庫層級的封裝管理：

   `RegisterRExt.exe /uninstallpkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]` 

    此命令會從指定的資料庫移除與封裝管理相關的資料庫成品。  此命令也會從 SQL Server 電腦上受保護的檔案系統位置，移除為每個資料庫安裝的所有封裝。
    
    此命令必須針對使用封裝管理所在的每個資料庫執行一次。
 
2. (選擇性) 若要從執行個體完全移除封裝管理功能，請在使用上述步驟清除所有資料庫的封裝之後，從提升權限的命令提示字元執行下列命令：

    `RegisterRExt.exe /uninstallpkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    此命令會從 SQL Server 執行個體移除封裝管理所使用的執行個體層級成品。 


## <a name="see-also"></a>另請參閱
[SQL Server R 服務的 R 封裝管理](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md)