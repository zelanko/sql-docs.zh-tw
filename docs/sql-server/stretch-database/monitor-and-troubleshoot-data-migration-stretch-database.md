---
title: 監視及疑難排解資料移轉
ms.date: 06/14/2016
ms.service: sql-server-stretch-database
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Stretch Database, monitoring
- monitoring Stretch Database
ms.assetid: 06950858-8c02-4ec6-9c59-42b787316a2d
author: rothja
ms.author: jroth
ms.custom: seo-dt-2019
ms.openlocfilehash: d204c7acfbd8598a7cbb66a41dcf89915fc711ef
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "73843783"
---
# <a name="monitor-and-troubleshoot-data-migration-stretch-database"></a>監視和疑難排解資料移轉 (Stretch Database)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


  若要在 Stretch Database 監視器中監視資料移轉，請針對 SQL Server Management Studio 中的資料庫，選取 [工作 | Stretch | 監視]  。  
  
## <a name="check-the-status-of-data-migration-in-the-stretch-database-monitor"></a>在 Stretch Database 監視器中檢查資料移轉狀態  
 針對 SQL Server Management Studio 中的資料庫選取 [工作 | Stretch | 監視]  ，以開啟 Stretch Database 監視器並監視資料移轉。  
  
-   監視器的上半部會顯示啟用延展的 SQL Server 資料庫與遠端 Azure 資料庫的一般資訊。  
  
-   監視的下半部會顯示資料庫中每個已啟用延展的資料表資料移轉狀態。  
  
 ![Stretch Database 監視](../../sql-server/stretch-database/media/stretch-monitor.PNG "Stretch Database 監視")  
  
##  <a name="check-the-status-of-data-migration-in-a-dynamic-management-view"></a><a name="Migration"></a> 在動態管理檢視中檢查資料移轉狀態  
 開啟動態管理檢視 **sys.dm_db_rda_migration_status** 查看已移轉的批次和資料列數目。 如需詳細資訊，請參閱 [sys.dm_db_rda_migration_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/stretch-database-sys-dm-db-rda-migration-status.md)。  
  
##  <a name="troubleshoot-data-migration"></a><a name="Firewall"></a> 對資料移轉進行疑難排解  
 **已啟用 Stretch 之資料表中的資料列沒有移轉到 Azure。發生什麼問題？**  
 有幾個問題會影響移轉。 請檢查下列事項。  
  
-   檢查 SQL Server 電腦的網路連線。  
  
-   檢查 Azure 防火牆沒有阻擋您的 SQL Server 連線到遠端端點。  
  
-   查看動態管理檢視 **sys.dm_db_rda_migration_status** 以取得最新批次的狀態。 如果發生錯誤，請檢查批次的 error_number、error_state 和 error_severity 各值。  
  
    -   如需檢視的詳細資訊，請參閱 [sys.dm_db_rda_migration_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/stretch-database-sys-dm-db-rda-migration-status.md)。  
  
    -   如需 SQL Server 錯誤訊息內容的詳細資訊，請參閱 [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)。  
  
 **Azure 防火牆封鎖了我的本機伺服器連線。**  
 您可能必須在 Azure 伺服器的 Azure 防火牆設定中新增一個規則，讓 SQL Server 與遠端 Azure 伺服器進行通訊。  
  
## <a name="see-also"></a>另請參閱  
 [管理 Stretch Database 並對其進行疑難排解](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md)  
  
  
