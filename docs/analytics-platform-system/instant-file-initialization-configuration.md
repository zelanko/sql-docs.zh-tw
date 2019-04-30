---
title: 設定立即檔案初始化-Analytics Platform System |Microsoft Docs
description: Analytics Platform System 上設定檔案立即初始化。 立即檔案初始化是 SQL Server 功能，可讓資料更快速執行的檔案作業。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 959d219565de6577e31d9548f5daea0fe0d2419e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63298128"
---
# <a name="instant-file-initialization-configuration"></a>檔案立即初始化設定
立即檔案初始化是 SQL Server 功能，可讓資料更快速執行的檔案作業。 核取方塊，若要開啟立即檔案初始化會改善效能的 SQL Server PDW。 不過，如果這有安全性風險，商務，然後核取方塊。  
  
> [!IMPORTANT]  
> 啟用立即檔案初始化時，SQL Server 不會覆寫已刪除的位元為零。  如果未經授權的使用者存取已刪除的資料，此行為可以建立安全性弱點。 不過，SQL Server PDW 可降低此風險確保 SQL Server 資料庫和備份檔案永遠連接到 SQL Server; 的執行個體只有 SQL Server 服務帳戶和本機系統管理員可以存取 SQL Server PDW 上已刪除的資料。  
  
當 TDE 啟用時，無法使用立即檔案初始化。  
  
## <a name="add-permission-for-the-backup-account"></a>新增備份的帳戶權限  
備份程序需要可以存取的備份儲存體位置的網路認證 （Windows 使用者帳戶）。 您授權，讓她能夠使用的帳戶使用 PDW [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)程序。 請參閱[BACKUP DATABASE](../t-sql/statements/backup-database-parallel-data-warehouse.md)整個備份程序。 若要使用立即檔案初始化，必須被授與備份帳戶`Perform volume maintenance tasks`權限。  
  
1.  在備份伺服器上，開啟**本機安全性原則**應用程式 (`secpol.msc`)。  
  
2.  在左窗格中，展開 [本機原則] ，然後按一下 [使用者權限指派] 。  
  
3.  在右窗格中，按兩下 [執行磁碟區維護工作]。  
  
4.  按一下 [新增使用者或群組]  ，新增用於備份的任何使用者帳戶。  
  
5.  按一下 [套用] ，然後關閉所有 [本機安全性原則]  對話方塊。  
  
## <a name="to-turn-instant-file-initialization-on-or-off"></a>若要開啟或關閉，請開啟立即檔案初始化  
  
1.  啟動組態管理員。 如需詳細資訊，請參閱 <<c0> [ 啟動組態管理員 &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)。</c0>  
  
2.  在左窗格的 Configuration Manager 中，按一下**立即檔案初始化**。  
  
3.  若要開啟立即檔案初始化，請選取方塊旁**所有節點上啟用立即檔案初始化**。 若要關閉檔案立即初始化，請清除方塊旁**所有節點上啟用立即檔案初始化**。  
  
    > [!WARNING]  
    > 當您關閉檔案立即初始化時，上面所討論之功能的安全性考量可能仍然會套用到檔案刪除，但已啟用檔案立即初始化。  
  
4.  按一下 **[套用]**。 下一次重新啟動設備服務時，就會透過 SQL Server PDW 上的 SQL Server 執行個體傳播變更。 若要立即重新啟動的應用裝置的服務，請參閱[PDW 服務狀態&#40;Analytics Platform System&#41;](pdw-services-status.md)。  
  
5.  您可能想要重複上述的步驟**備份帳戶的 新增權限**移除**執行磁碟區維護工作**權限。  
  
![DWConfig 應用裝置 PDW 立即檔案初始化](./media/instant-file-initialization-configuration/SQL_Server_PDW_DWConfig_ApplPDWInstant.png "SQL_Server_PDW_DWConfig_ApplPDWInstant")  
  
如需有關立即檔案初始化的詳細資訊，請參閱 <<c0> [ 立即檔案初始化](https://technet.microsoft.com/library/ms175935(v=SQL.105).aspx)。  
  
