---
title: "記錄傳送交易記錄備份設定 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: log-shipping
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.databaseproperties.logshipping.settings.tlogback.f1
ms.assetid: 9a6e6c16-7f71-412b-bba6-7bffac001277
caps.latest.revision: "27"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 01a15e3ebf54cae459aad00052e009774d125c56
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="log-shipping-transaction-log-backup-settings"></a>記錄傳送交易記錄備份設定
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 使用此對話方塊來設定和修改記錄傳送設定的交易記錄備份設定。  
  
 如需記錄傳送概念的說明，請參閱 [關於記錄傳送 &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)。  
  
## <a name="options"></a>選項。  
 **備份資料夾的網路路徑**  
 在此方塊中輸入備份資料夾的網路共用。 儲存交易記錄備份的本機資料夾必須共用，記錄傳送複製作業才能將這些檔案複製至次要伺服器。 您必須將此網路共用的讀取權限授與 Proxy 帳戶，在此帳戶下，複製作業將會在次要伺服器執行個體上執行。 依預設，這是次要伺服器執行個體的 SQLServerAgent 服務帳戶，但是管理員可以為此作業選擇另一個 Proxy 帳戶。  
  
 **如果備份資料夾位於主要伺服器上，請輸入該資料夾的本機路徑**  
 如果備份資料夾位於主要伺服器上，請輸入備份資料夾的本機磁碟機代號和路徑。 如果備份資料夾不在主要伺服器上，您可以讓此欄位保留空白。  
  
 如果您在此指定本機路徑，則 BACKUP 命令將使用此路徑來建立交易記錄備份；否則，如果未指定本機路徑，BACKUP 命令將使用 [備份資料夾的網路路徑] 方塊中所指定的網路路徑。  
  
> [!NOTE]  
>  如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶是在主要伺服器的本機系統帳戶之下執行，您就必須在主要伺服器上建立備份資料夾，然後在此指定該資料夾的本機路徑。 主要伺服器執行個體的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶必須擁有此資料夾的讀取和寫入權限。  
  
 **指定刪除檔案的時限**  
 指定在刪除之前要讓交易記錄備份維持在備份目錄中的時間長度。  
  
 **如果未在此時間內進行備份，則發出警示**  
 指定在引發未發生交易記錄備份的警示之前，您要記錄傳送等候的時間量。  
  
 **作業名稱**  
 顯示用來建立記錄傳送之交易記錄備份的 SQL Server Agent 作業的名稱。 首次建立作業時，您可以在此方塊中輸入名稱來修改其名稱。  
  
 **[排程]**  
 顯示備份主要資料庫之交易記錄的目前排程。 建立備份作業之前，按一下 [排程...] 即可修改此排程。建立備份作業之後，按一下 [編輯作業...] 即可修改此排程。  
  
### <a name="backup-job"></a>備份作業  
 **排程...**  
 修改建立 SQL Server Agent 作業時所建立的排程。  
  
 **編輯作業...**  
 修改在主要資料庫上執行交易記錄備份之作業的 SQL Server Agent 作業參數。  
  
 **停用此作業**  
 使 SQL Server Agent 作業不能建立交易記錄備份。  
  
### <a name="compression"></a>壓縮  
 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] (或更新版本) 支援 [備份壓縮](../../relational-databases/backup-restore/backup-compression-sql-server.md)。  
  
 **設定備份壓縮**  
 在 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] (或更新的版本) 中，針對此記錄傳送設定的記錄備份選取下列其中一個備份壓縮值：  
  
|||  
|-|-|  
|**使用預設伺服器設定**|按一下即可使用伺服器層級的預設值。<br /><br /> 此預設值是由 [備份壓縮預設] 伺服器組態選項所設定。 有關如何檢視這個選項目前之設定的詳細資訊，請參閱 [檢視或設定備份壓縮預設伺服器組態選項](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)。|  
|**壓縮備份**|不論目前的伺服器層級預設值為何，按一下即可壓縮備份。<br /><br /> **\*\* 重要事項 \*\*** 根據預設，壓縮會大幅增加 CPU 使用量，而且壓縮程序所耗用的額外 CPU 可能會對並行作業造成不良的影響。 因此，您可能會想要在 [資源管理員](../../relational-databases/resource-governor/resource-governor.md)限制 CPU 使用量的工作階段中，建立低優先權的壓縮備份。 如需詳細資訊，請參閱本主題稍後介紹的＜ [使用資源管理員進行備份壓縮，以限制 CPU 使用率 &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)限制的工作階段中，建立低優先權的壓縮備份。|  
|**不要壓縮備份**|不論目前的伺服器層級預設值為何，按一下即可建立未壓縮備份。|  
  
## <a name="see-also"></a>另請參閱  
 [設定使用者可建立及管理 SQL Server Agent 作業](http://msdn.microsoft.com/library/67897e3e-b7d0-43dd-a2e2-2840ec4dd1ef)   
 [關於記錄傳送 &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)  
  
  
