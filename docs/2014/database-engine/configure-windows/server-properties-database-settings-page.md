---
title: 伺服器屬性 (資料庫設定頁面) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.serverproperties.databasesettings.f1
ms.assetid: 1cebdbd3-cbfd-4a02-bba6-a5addf4e3ada
caps.latest.revision: 31
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 9d44381ef0af703efb104a38f5eeebf99fc21ff7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031969"
---
# <a name="server-properties-database-settings-page"></a>伺服器屬性 (資料庫設定頁面)
  使用此頁面來檢視或修改您的資料庫設定。  
  
## <a name="options"></a>選項。  
 **預設索引填滿因數**  
 指定當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用現有的資料建立新索引時，它應該填入每個頁面的程度。 填滿因數會影響效能，因為當頁面填滿之後， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 就必須花費時間進行頁面的分割。  
  
 預設值是 0，有效值的範圍是從 0 到 100。 填滿因數 0 或 100 會以完整分葉頁面建立有完整資料頁面和非叢集索引的叢集索引，但是會在索引樹狀結構的上層保留部分空間。 從各方面來說，填滿因數值 0 和 100 都相同。  
  
 較小的填滿因數值會使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 建立不完全填滿頁面的索引。 每一個索引佔用更多的儲存空間，但後續可以有更多插入空間，不需要再分割頁面。  
  
 **永遠等候**  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在等候新備份磁帶時永不逾時。  
  
 **嘗試一次**  
 指定如果需要備份磁帶卻無法使用時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會逾時。  
  
 **嘗試分鐘數**  
 指定如果在指定期間內沒有備份磁帶可用時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會逾時。  
  
 **預設備份媒體保留 (以天為單位)**  
 提供每個備份媒體的全系統保存預設時間長度，設定當備份用於資料庫或交易記錄備份之後，預設要保存多久。 此選項協助保護備份，在指定的天數經過之前不被覆寫。  
  
 **壓縮備份**  
 在 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] (或更新的版本) 中，表示 [備份壓縮預設] 選項的目前設定。 這一個選項會決定壓縮備份的伺服器層級預設值，如下所示：  
  
-   如果 **[壓縮備份]** 方塊是空的，新備份預設不會進行壓縮。  
  
-   如果 **[壓縮備份]** 方塊已核取，新備份預設就會進行壓縮。  
  
    > [!IMPORTANT]  
    >  根據預設，壓縮會大幅增加 CPU 使用量，而且壓縮程序所耗用的額外 CPU 可能會對並行作業造成不良的影響。 因此，您可能會想要在由[資源管理員](../../relational-databases/resource-governor/resource-governor.md)所限制之 CPU 使用量的工作階段中建立低優先權的壓縮備份。 如需詳細資訊，請參閱本主題稍後介紹的＜ [使用資源管理員進行備份壓縮，以限制 CPU 使用率 &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)限制的工作階段中，建立低優先權的壓縮備份。  
  
 如果您是 **系統管理員 (sysadmin)** 或 **serveradmin** 固定伺服器角色的成員，您可以透過按一下 [壓縮備份]  方塊，變更設定。  
  
 如需詳細資訊，請參閱[檢視或設定 backup compression default 伺服器組態選項](view-or-configure-the-backup-compression-default-server-configuration-option.md)和[備份壓縮 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-compression-sql-server.md)。  
  
 **復原間隔 (分鐘)**  
 設定每個資料庫復原的最長時間 (分鐘)。 預設值是 0，指出由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]自動組態。 實務上，這表示復原時間小於一分鐘，而且使用中資料庫幾乎每分鐘有一次檢查點。 如需詳細資訊，請參閱 [Configure the recovery interval Server Configuration Option](configure-the-recovery-interval-server-configuration-option.md)。  
  
 **資料**  
 指定資料檔案的預設位置。 按一下 [瀏覽] 按鈕，即可導覽到新的預設位置。 要等到重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之後才會生效。  
  
 **Log**  
 指定記錄檔案的預設位置。 按一下 [瀏覽] 按鈕，即可導覽到新的預設位置。 要等到重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之後才會生效。  
  
 **設定的值**  
 針對此窗格中的選項，顯示設定的值。 如果您變更這些值，請按一下 **[執行中的值]** ，即可查看變更是否已生效。 如果沒有的話，就必須先重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。  
  
 **[執行中的值]**  
 針對此窗格中的選項，檢視目前執行中的值。 這些值是唯讀的。  
  
## <a name="see-also"></a>另請參閱  
 [伺服器組態選項 &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [指定索引的填滿因素](../../relational-databases/indexes/specify-fill-factor-for-an-index.md)  
  
  