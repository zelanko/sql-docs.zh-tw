---
title: "立即檔案初始化組態 (Analytics Platform System)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 58be8982-4d2e-4aa3-bcdd-874a062d2f9d
caps.latest.revision: "20"
ms.openlocfilehash: b7dda4bb925e08f49409ea1950cfe3649b4db3e0
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="instant-file-initialization-configuration"></a>立即檔案初始化組態
立即檔案初始化是 SQL Server 功能，可讓資料檔案作業更快速地執行。 核取方塊，若要開啟立即檔案初始化會改善 SQL Server PDW 的效能。 不過，如果這會有安全性風險，商務，然後不要選取這個方塊。  
  
> [!IMPORTANT]  
> 啟用立即檔案初始化時，SQL Server 不會覆寫已刪除的位元加上零。  如果未經授權的使用者存取已刪除的資料，此行為可以建立安全性弱點。 不過，SQL Server PDW 可以降低此風險確保 SQL Server 資料庫和備份檔案永遠附加至執行個體的 SQL Server;只有 SQL Server 服務帳戶和本機系統管理員可以存取 SQL Server PDW 上已刪除的資料。  
  
當 TDE 啟用時，無法使用立即檔案初始化。  
  
## <a name="add-permission-for-the-backup-account"></a>新增備份的帳戶權限  
備份程序需要網路認證 （Windows 使用者帳戶） 可以存取的備份儲存位置。 授權使用的帳戶，方法是使用 PDW [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)程序。 請參閱[備份資料庫](../t-sql/statements/backup-database-parallel-data-warehouse.md)針對整個備份程序。 若要使用立即檔案初始化，必須授與備份帳戶`Perform volume maintenance tasks`權限。  
  
1.  備份伺服器上，開啟**本機安全性原則**應用程式 (`secpol.msc`)。  
  
2.  在左窗格中，展開 [本機原則] ，然後按一下 [使用者權限指派] 。  
  
3.  在右窗格中，按兩下 [執行磁碟區維護工作]。  
  
4.  按一下 [新增使用者或群組]  ，新增用於備份的任何使用者帳戶。  
  
5.  按一下 [套用] ，然後關閉所有 [本機安全性原則]  對話方塊。  
  
## <a name="to-turn-instant-file-initialization-on-or-off"></a>若要開啟或關閉開啟立即檔案初始化  
  
1.  啟動 Configuration Manager。 如需詳細資訊，請參閱[啟動組態管理員 &#40;Analytics Platform System &#41;](launch-the-configuration-manager.md).  
  
2.  在左窗格的 Configuration Manager 中，按一下 **立即檔案初始化**。  
  
3.  若要開啟立即檔案初始化，請選取方塊旁的 **所有節點上啟用立即檔案初始化**。 若要關閉立即檔案初始化，請清除方塊旁的 **所有節點上啟用立即檔案初始化**。  
  
    > [!WARNING]  
    > 當您關閉立即檔案初始化時，上面所討論之功能的安全性考量可能仍然會套用到啟用立即檔案初始化已刪除的檔案。  
  
4.  按一下 **[套用]**。 下一次應用裝置服務重新啟動時，會透過 SQL Server PDW 上的 SQL Server 執行個體傳播變更。 若要立即重新啟動的應用裝置的服務，請參閱[PDW 服務狀態 &#40;Analytics Platform System &#41;](pdw-services-status.md).  
  
5.  您可能想要重複上述步驟**加入備份帳戶的權限**移除**執行磁碟區維護工作**權限。  
  
![DWConfig 應用裝置 PDW 立即檔案初始化](./media/instant-file-initialization-configuration/SQL_Server_PDW_DWConfig_ApplPDWInstant.png "SQL_Server_PDW_DWConfig_ApplPDWInstant")  
  
如需有關立即檔案初始化的詳細資訊，請參閱[立即檔案初始化](http://technet.microsoft.com/en-us/library/ms175935(v=SQL.105).aspx)。  
  
