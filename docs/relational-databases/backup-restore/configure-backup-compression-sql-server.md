---
title: "設定備份壓縮 (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: backup-restore
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 430905eb-d218-458c-bd48-aeee6fbb7446
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 43f1fbed7a953bf8989764c9c835a047fb65d4c2
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="configure-backup-compression-sql-server"></a>設定備份壓縮 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 進行安裝時，備份壓縮預設是關閉的。 備份壓縮的預設行為是透過 [備份壓縮預設] 伺服器層級組態選項所定義。 不過，您可以在建立單一備份或排程一系列例行備份時，覆寫此伺服器層級預設值。 若要變更伺服器層級的預設值，請參閱 [檢視或設定備份壓縮預設伺服器組態選項](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)。  
  
## <a name="override-the-backup-compression-default"></a>覆寫備份壓縮預設  
 您可以針對個別的備份、備份作業或記錄傳送組態來變更備份壓縮行為。  
  
-   **[!INCLUDE[tsql](../../includes/tsql-md.md)]**  
  
     若要在建立備份時覆寫伺服器備份壓縮預設，請在 [BACKUP](../../t-sql/statements/backup-transact-sql.md) 陳述式中使用 WITH NO_COMPRESSION 或 WITH COMPRESSION。  
  
     如果是記錄傳送設定，您可以使用 [sp_add_log_shipping_primary_database](../../relational-databases/system-stored-procedures/sp-add-log-shipping-primary-database-transact-sql.md)[sp_change_log_shipping_primary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-log-shipping-primary-database-transact-sql.md) 來控制記錄備份的備份壓縮行為。  
  
-   **[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
     如需如何檢視或設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體之 [備份壓縮預設] 選項的資訊，請參閱[檢視或設定備份壓縮預設伺服器組態選項](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)。  
  
     在下列任何對話方塊中指定 [壓縮備份] 或 [不要壓縮備份]，就可以在建立備份時覆寫伺服器備份壓縮預設：  
  
    -   [備份資料庫 (選項頁面)](../../relational-databases/backup-restore/back-up-database-backup-options-page.md)  
  
         在備份資料庫時，您可以控制個別資料庫、檔案或記錄備份的備份壓縮。  
  
    -   [使用維護計畫精靈](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)  
  
         「維護計畫精靈」可讓您針對每個排程的完整或差異資料庫備份或記錄備份，控制備份壓縮。  
  
    -   Integration Services (SSIS) [備份資料庫工作](../../integration-services/control-flow/back-up-database-task.md)  
  
         針對備份單一資料庫或多個資料庫建立封裝時，您可以控制備份壓縮行為。  
  
    -   [記錄傳送交易記錄備份設定](../../relational-databases/databases/log-shipping-transaction-log-backup-settings.md)  
  
         您可以控制記錄備份的備份壓縮行為。  
  
  
## <a name="see-also"></a>另請參閱  
 [備份壓縮 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-compression-sql-server.md)  
  
  
