---
title: 設定管理資料倉儲 (SSMS)
description: 了解如何設定管理資料倉儲，以便支援使用資料收集器之一或多個 SQL Server 執行個體的資料儲存體。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql13.swb.dc.datacollection.wizard_completecfg.f1
- sql13.swb.dc.datacollection.wizard_config.f1
- sql13.swb.dc.datacollection.wizard_finish.f1
- sql13.swb.dc.datacollection.wizard_maploginuser.f1
- sql13.swb.dc.datacollection.wizard_choosemdw.f1
- sql13.swb.dc.datacollection.wizard_welcome.f1
- sql13.swb.dc.datacollection.wizard_createmdw.f1
helpviewer_keywords:
- data warehouse [SQL Server], multiple instances
- data warehouse [SQL Server], configuring
- Configure Management Data Warehouse Wizard
- management data warehouse, configuring
ms.assetid: 23a584f3-c5e1-414c-9afe-73cd7efbda4b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1c82c79bcf0b1494890055c098e6c7efdbc733ee
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85733869"
---
# <a name="configure-the-management-data-warehouse-sql-server-management-studio"></a>設定管理資料倉儲 (SQL Server Management Studio)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  此主題描述如何設定管理資料倉儲，以支援使用資料收集器之一個或多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的資料儲存體。 這些執行個體可以在相同伺服器或不同伺服器上。 此主題也提供 [設定管理資料倉儲精靈](#Wizard) 對話方塊的使用者介面描述。 如需設定資料收集器的詳細資訊，請參閱＜ [Configure Properties of a Data Collector](../../relational-databases/data-collection/configure-properties-of-a-data-collector.md)＞。  
  
> [!NOTE]  
>  如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 設定成使用其中一個系統服務帳戶 (本機系統、網路服務或本機服務) 來執行，而且管理資料倉儲是從資料收集器的另一個執行個體建立，您就必須設定收集組使用 Proxy 將資料上傳到管理資料倉儲。  
  
### <a name="configure-the-management-data-warehouse-on-a-single-instance-or-multiple-instances-of-ssnoversion"></a>在一個或多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
1.  確定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 正在執行中。  
  
2.  在 [物件總管] 中，展開 **[管理]** 節點。  
  
3.  以滑鼠右鍵按一下 [資料收集]，展開 [工作]，然後按一下 [設定管理資料倉儲]。  
  
4.  使用 [設定管理資料倉儲精靈](#Wizard) 來建立管理資料倉儲、設定登入、啟用資料收集，並啟動 **[系統資料收集組]** 。  
  
     若要設定多個執行個體，請繼續執行步驟 5。  
  
    > [!NOTE]  
    >  公認的最佳作法是將 Proxy 用於在多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體 (使用相同的管理資料倉儲) 上安裝資料收集器的部署中。  
  
5.  在另一個執行個體上開啟 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，然後進行下列任何一項動作：  
  
    -   使用「設定管理資料倉儲精靈」來針對現有的管理資料倉儲設定資料收集。  
  
    -   以滑鼠右鍵按一下 [資料收集]，然後按一下 [屬性]。 在 **[一般]** 索引標籤中，指定現有的管理資料倉儲以及它安裝所在的伺服器。  
  
6.  重複步驟 5，直到使用資料收集器的所有資料庫執行個體都設定為可將資料上傳到共用管理資料倉儲為止。  

####  <a name="configure-management-data-warehouse-wizard"></a><a name="Wizard"></a> 設定管理資料倉儲精靈  
 **歡迎頁面**  
  
 此歡迎頁面是「設定資料收集精靈」的起始頁面。 可以選擇是否顯示此頁面。  
  
 **不要再顯示此開始頁面。**  
 選取此選項，可在下一次啟動「設定資料收集精靈」時隱藏這個頁面。  
  
 **設定管理資料倉儲儲存體頁面**  
  
 使用這個頁面可選取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫伺服器和管理資料倉儲。 管理資料倉儲是一種關聯式資料庫，它將會儲存收集而來的資料。  
  
> [!NOTE]  
>  您必須具備適當的權限等級，才能在伺服器上建立管理資料倉儲。 如需詳細資訊，請參閱 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)。 您也必須具備適當的權限等級，才能建立管理資料倉儲角色的登入。  
  
 **伺服器名稱**  
 指定將主控管理資料倉儲的伺服器名稱。  
  
 在設定管理資料倉儲時， **[伺服器名稱]** 永遠是本機伺服器的名稱，而且無法修改。  
  
 **資料庫名稱**  
 指定將會儲存收集之資料的關聯式資料庫。 使用此清單來選取現有的資料庫，或是使用 **[新增資料庫]** 對話方塊來按一下 **[新增]** ，建立新的資料庫。  
  
 **[新增]** 選項只有在設定資料收集組時才提供。  
  
 **對應登入及使用者頁面**  
  
 使用這個頁面可將登入對應到管理資料倉儲的資料庫使用者角色。  
  
 **已對應到此登入的使用者**  
 顯示伺服器上將主控管理資料倉儲的現有登入。 每一個資料列都包含可編輯的 **[對應]** 核取方塊、 **[登入]** 名稱和登入的 **[類型]** 。  
  
 為登入選取 **[對應]** 核取方塊來指定此登入。  
  
 **資料庫角色成員資格對象:**  *\<data warehouse name>*  
 選取此登入所對應的管理資料倉儲角色，其方式是按一下下列一或多個選項旁邊的核取方塊：  
  
-   **mdw_admin**  
  
-   **mdw_reader**  
  
-   **mdw_writer**  
  
 **新增登入**  
 開啟 [登入 - 新增] 對話方塊，並為此管理資料倉儲建立新的登入。  
  
 **完成精靈頁面**  
  
 使用此頁面可驗證及完成資料收集組態。 檢視視窗中所顯示的樹狀目錄會顯示將要套用哪些組態，以及當您按一下 **[完成]** 時將會發生的動作。  
  
 **設定資料收集精靈進度頁面**  
  
 使用此頁面可檢視每一個組態步驟的結果。  
  
 **詳細資料**  
 將每一個組態步驟顯示為 [詳細資料] 方格中的資料列。 每一個資料列都包含一個可描述此步驟的 **[動作]** 資料行，以及一個指示此步驟為成功或失敗的 **[狀態]** 資料行。 如果發生錯誤， **[訊息]** 資料行中會出現訊息。  
  
 **停止**  
 停止精靈的處理。  
  
 **Report**  
 檢視資料收集組態的報表。 以下是提供的報表選項：  
  
-   檢視報表  
  
-   將報表儲存到檔案  
  
-   [複製報表到剪貼簿]  
  
-   以電子郵件傳送報表  
  
 **關閉**  
 關閉精靈。  
  
## <a name="see-also"></a>另請參閱  
 [sp_syscollector_enable_collector &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-enable-collector-transact-sql.md)   
 [sp_syscollector_disable_collector &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-disable-collector-transact-sql.md)   
 [資料收集](../../relational-databases/data-collection/data-collection.md)   
 [管理資料收集](../../relational-databases/data-collection/manage-data-collection.md)  
  
  
