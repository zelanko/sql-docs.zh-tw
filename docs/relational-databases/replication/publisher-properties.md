---
title: SQL Server 複寫發行者屬性對話方塊 | Microsoft Docs
ms.custom: ''
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.configdistwizard.distpubproperties.f1
- sql13.rep.configdistwizard.pubproperties.general.f1
- sql13.rep.configdistwizard.pubproperties.pubdb.f1
- sql13.rep.configdistwizard.pubproperties.subscribers.f1
ms.assetid: 98df1aea-0406-40bf-a917-4bd80464125c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: aa39a4752952a3d214d7dea8eaeb236c75d9f5d5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68021324"
---
# <a name="sql-server-replication-publisher-properties-dialog-box"></a>SQL Server 複寫發行者屬性對話方塊
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本主題說明 [發行者屬性] 對話方塊內的各種不同選項。 

## <a name="general"></a>一般
  **[發行者屬性]** 對話方塊的 **[一般]** 頁面，會顯示散發者與發行者所使用之散發資料庫的唯讀資訊。 若要變更散發者或發行者的散發資料庫：  
  
1.  在發行者上停用發行。 如需詳細資訊，請參閱[停用發行和散發](../../relational-databases/replication/disable-publishing-and-distribution.md)。    
2.  重新設定發行和散發。 如需詳細資訊，請參閱 [Configure Publishing and Distribution](../../relational-databases/replication/configure-publishing-and-distribution.md)。  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="distributor"></a>散發者 
**[發行者屬性]** 對話方塊可讓您檢視和修改與發行者及其散發者之間的關聯性相關聯的屬性。  
  
### <a name="options"></a>選項。  
 **代理程式至發行者的連接**  
 指定下列代理程式用來從散發者連接到發行者的內容。  
  
-   允許佇列更新訂閱之交易式發行集的佇列讀取器代理程式。    
-   Oracle 發行集的快照集代理程式和記錄讀取器代理程式。  
  
 選取 **[模擬代理程式處理帳戶]** 來使用執行這些代理程式的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帳戶連接到發行者，或指定 **[SQL Server 驗證]** ，然後輸入 **[登入]** 和 **[密碼]** 的值。 建議您選取 **[模擬代理程式處理帳戶]** 。 如需代理程式安全性的詳細資訊，請參閱[複寫代理程式安全性模型](../../relational-databases/replication/security/replication-agent-security-model.md)。  
  
 執行這些代理程式的 Windows 帳戶會在新增發行集精靈中指定。 可以在下列位置變更這些帳戶：  
  
-   在佇列讀取器代理程式的 **[散發者屬性]** 對話方塊中。    
-   在快照集代理程式和記錄讀取器代理程式的 **[發行集屬性]** 對話方塊中。  
  
 **其他**  
 屬性 **[發行者類型]** 和 **[散發資料庫名稱]** 是唯讀的。 可以變更屬性 **[預設快照集資料夾]** 。 如需快照集資料夾的詳細資訊，請參閱[保護快照集資料夾](../../relational-databases/replication/security/secure-the-snapshot-folder.md)。  

## <a name="publication-databases"></a>發行集資料庫
  **[發行者屬性]** 對話方塊的 **[發行集資料庫]** 頁面，可讓 **系統管理員 (sysadmin)** 固定伺服器角色中的使用者啟用資料庫供複寫。 啟用資料庫不會發行此資料庫；不過，它允許該資料庫之 **db_owner** 固定資料庫角色中的任何使用者在資料庫上建立一個或多個發行集。  
  
## <a name="options"></a>選項。  
 **異動**  
 選取此核取方塊即可讓 **db_owner** 固定資料庫角色中的使用者，在資料庫中建立快照式發行集或交易式發行集。 
  
 **合併式**  
 選取此核取方塊即可讓 **db_owner** 固定資料庫角色中的使用者，在資料庫中建立合併式發行集。  
  

## <a name="subcribers"></a>訂閱者
  [發行者屬性]  對話方塊的 [訂閱者]  頁面，是用於執行 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 之前的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本之發行者。 此頁面可讓您啟用訂閱者，以接收來自此發行者的發行集資料。 啟用訂閱者以接收來自此發行者的資料，並不會在此發行者上建立發行集的訂閱。 若要建立訂閱，您必須使用新增訂閱精靈。  
  
### <a name="options"></a>選項。  
 **[發行者屬性]**  
 **[訂閱者]** 屬性方格，會顯示已啟用來接收此發行者之發行集資料的訂閱者。 按一下訂閱者旁的屬性按鈕 ( **...** )，即可檢視和設定其他屬性。  
  
 **[加入]**  
 按一下 **[加入]** 即可加入訂閱者，然後按一下 **[加入 SQL Server 訂閱者]** 或 **[加入非 SQL Server 訂閱者]** 。  
  
## <a name="see-also"></a>另請參閱  
 [檢視及修改散發者和發行者屬性](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [建立發行集](../../relational-databases/replication/publish/create-a-publication.md)   


  
