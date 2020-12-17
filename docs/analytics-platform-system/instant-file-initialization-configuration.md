---
title: 設定檔案立即初始化
description: 在 Analytics Platform System 上設定立即檔案初始化。 立即檔案初始化是 SQL Server 的功能，可讓資料檔案作業更快速地執行。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 6843efa430fcd43149d048c9d21c5120954ab896
ms.sourcegitcommit: 370cab80fba17c15fb0bceed9f80cb099017e000
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/17/2020
ms.locfileid: "97637814"
---
# <a name="instant-file-initialization-configuration"></a>立即檔案初始化設定
立即檔案初始化是 SQL Server 的功能，可讓資料檔案作業更快速地執行。 核取開啟 [立即檔案初始化] 的方塊，將可改善 SQL Server PDW 的效能。 但是，如果這對您的業務造成安全性風險，請將此方塊保留為未核取。  
  
> [!IMPORTANT]  
> 當立即檔案初始化啟用時，SQL Server 不會將已刪除的位覆寫為零。  如果未經授權的使用者取得已刪除資料的存取權，這種行為可能會產生安全性弱點。 不過，SQL Server PDW 藉由確保 SQL Server 資料庫和備份檔案一律附加至 SQL Server 的實例，來降低這項風險;只有 SQL Server 服務帳戶和本機系統管理員可以存取 SQL Server PDW 上已刪除的資料。  
  
當 TDE 啟用時，無法使用立即檔案初始化。  
  
## <a name="add-permission-for-the-backup-account"></a>新增備份帳戶的許可權  
備份程式需要 (Windows 使用者帳戶) 的網路認證，才能存取備份儲存位置。 您會授權 PDW 使用 [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) 程式來使用帳戶。 請參閱 [備份資料庫](../t-sql/statements/backup-transact-sql.md) 以取得整個備份程式。 若要使用立即檔案初始化，必須將許可權授與備份帳戶 `Perform volume maintenance tasks` 。  
  
1.  在備份伺服器上，開啟 [ **本機安全性原則** ] 應用程式 (`secpol.msc`) ]。  
  
2.  在左窗格中，展開 [本機原則] ，然後按一下 [使用者權限指派] 。  
  
3.  在右窗格中，按兩下 [執行磁碟區維護工作]。  
  
4.  按一下 [新增使用者或群組]  ，新增用於備份的任何使用者帳戶。  
  
5.  按一下 [套用] ，然後關閉所有 [本機安全性原則]  對話方塊。  
  
## <a name="to-turn-instant-file-initialization-on-or-off"></a>開啟或關閉立即檔案初始化  
  
1.  啟動 Configuration Manager。 如需詳細資訊，請參閱 [啟動 Configuration Manager &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)。  
  
2.  在 Configuration Manager 的左窗格中，按一下 [ **立即檔案初始化**]。  
  
3.  若要開啟立即檔案初始化，請選取 [ **在所有節點上啟用立即檔案初始化**] 旁的方塊。 若要關閉立即檔案初始化，請清除 [ **在所有節點上啟用立即檔案初始化**] 旁的核取方塊。  
  
    > [!WARNING]  
    > 當您關閉 [立即檔案初始化] 時，上述針對此功能所討論的安全性考慮，可能仍會套用至 [立即檔案初始化] 啟用時所刪除的檔案。  
  
4.  按一下 [套用]  。 下次重新開機設備服務時，變更將會在 SQL Server PDW 的 SQL Server 實例之間傳播。 若要立即重新開機設備服務，請參閱 [PDW 服務狀態 &#40;Analytics Platform System&#41;](pdw-services-status.md)。  
  
5.  您可能會想要重複上述步驟，作為 **備份帳戶的新增許可權** ，以移除「 **執行磁片區維護** 工作」許可權。  
  
![DWConfig 應用裝置 PDW 立即檔案初始化](./media/instant-file-initialization-configuration/SQL_Server_PDW_DWConfig_ApplPDWInstant.png "SQL_Server_PDW_DWConfig_ApplPDWInstant")  
  
如需有關立即檔案初始化的詳細資訊，請參閱 [立即檔案初始化](/previous-versions/sql/sql-server-2008-r2/ms175935(v=sql.105))。  
