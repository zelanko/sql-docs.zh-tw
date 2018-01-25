---
title: "升級複寫指令碼 (複寫 Transact-SQL 程式設計) | Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: TSQL
helpviewer_keywords:
- scripts [SQL Server replication], upgrading
- upgrading SQL Server, replicated databases
- upgrading replication applications
- replication [SQL Server], scripting
- replication [SQL Server], upgrading
- upgrading replicated databases
ms.assetid: 0b8720bd-f339-4842-bc8f-b35a46f6d3ee
caps.latest.revision: "41"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 09f8ed7bf8cbd407a8bd9dc706d5e9aadf34ce65
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="upgrade-replication-scripts-replication-transact-sql-programming"></a>升級複寫指令碼 (複寫 Transact-SQL 程式設計)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] [!INCLUDE[tsql](../../../includes/tsql-md.md)] 指令碼檔案可以用於以程式設計的方式設定複寫拓撲。 如需詳細資訊，請參閱[複寫系統預存程序概念](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)。  
  
> [!IMPORTANT]  
>  雖然並不一定要升級由 **sysadmin** 角色的成員所執行的指令碼，但建議您依照本主題所述修改現有的指令碼。 請根據主題＜ [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md)＞的「代理程式所需的權限」一節所述，為每個複寫代理程式指定具有最小權限的帳戶。  
  
 這些安全性改進會影響現有指令碼中的下列預存程序，讓您可以明確地指定 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 帳戶，並在這些帳戶下執行複寫代理程式工作，對權限可以有更多的控制：  
  
-   **sp_addpublication_snapshot**:  
  
     現在當您執行 [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md) 時，應該以 **@job_login** 和 **@job_password** 提供 Windows 認證，以建立在散發者端執行快照集代理程式的作業。  
  
-   **sp_addpushsubscription_agent**：  
  
     現在應該執行 [sp_addpushsubscription_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md) 以明確地新增作業並提供 Windows 認證 (**@job_login** 和 **@job_password**)，藉此在散發者端執行散發代理程式作業。 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]版本中，這項作業會在建立發送訂閱時自動完成。  
  
-   **sp_addmergepushsubscription_agent**：  
  
     現在應該執行 [sp_addmergepushsubscription_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md) 以明確地新增作業並提供 Windows 認證 (**@job_login** 和 **@job_password**)，藉此在散發者端執行合併代理程式作業。 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]版本中，這項作業會在建立發送訂閱時自動完成。  
  
-   **sp_addpullsubscription_agent**：  
  
     現在當您執行 [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md) 時，應該以 **@job_login** 和 **@job_password** 提供 Windows 認證，以建立在訂閱者端執行散發代理程式的作業。  
  
-   **sp_addmergepullsubscription_agent**：  
  
     現在當您執行 [sp_addmergepullsubscription_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md) 時，應該以 **@job_login** 和 **@job_password** 提供 Windows 認證，以建立在訂閱者端執行合併代理程式的作業。  
  
-   **sp_addlogreader_agent**：  
  
     現在應該執行 [sp_addlogreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md) 以手動新增作業並提供 Windows 認證，藉此在散發者端執行記錄讀取器代理程式。 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]版本中，這項作業會在建立交易式發行集時自動完成。  
  
-   **sp_addqreader_agent**：  
  
     現在應該執行 [sp_addqreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md) 以手動新增作業並提供 Windows 認證，藉此在散發者端執行佇列讀取器代理程式。 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]版本中，這項作業會在建立支援佇列更新的交易式發行集時自動完成。  
  
 在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]所導入的安全性模型中，複寫代理程式一定會使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] @job_name **@job_name** @job_login **@job_password**。 如需有關在執行複寫代理程式作業時所使用 Windows 帳戶之需求的資訊，請參閱＜ [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md)＞。  
  
> [!IMPORTANT]  
>  可能的話，會在執行階段提示使用者輸入安全性認證。 如果將認證儲存在指令碼檔案中，請確定該檔案本身受到安全保護。  
  
### <a name="to-upgrade-scripts-that-configure-a-snapshot-or-transactional-publication"></a>若要升級設定快照式或交易式發行集的指令碼  
  
1.  在現有指令碼的 [sp_addpublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) 之前，於發行集資料庫的發行者端執行 [sp_addlogreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)。 指定「Windows 認證」，「記錄讀取器代理程式」執行時會將該認證用於 **@job_name** @job_login **@job_password**。 如果代理程式會在與「發行者」時連接時使用「 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證」，則也必須指定 **@publisher_security_mode** 的值 **@publisher_security_mode** ，以及 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] @publisher_login **@publisher_login** @job_login **@publisher_password**。 如此會建立發行集資料庫的「記錄讀取器代理程式」作業。  
  
    > [!NOTE]  
    >  只有交易式發行集才需要這個步驟，快照式發行集不需要。  
  
2.  (選擇性) 在 [sp_addpublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) 之前，於散發資料庫的散發者端執行 [sp_addqreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md)。 指定「Windows 認證」，「佇列讀取器代理程式」執行時會將該認證用於 **@job_name** @job_login **@job_password**。 如此會為「散發者」建立「佇列讀取器代理程式」作業。  
  
    > [!NOTE]  
    >  只有支援佇列更新訂閱者的交易式發行集才需要這個步驟。  
  
3.  (選擇性) 更新 [sp_addpublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) 的執行，以針對實作新複寫功能的參數設定預設以外的值。  
  
4.  在 [sp_addpublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) 之後，於發行集資料庫的發行者端執行 [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)。 指定 **@publication** 和「Windows 認證」，「快照集代理程式」執行時會將該認證用於 **@job_name** @job_login **@job_password**。 如果代理程式會在與「發行者」時連接時使用「 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證」，則也必須指定 **@publisher_security_mode** 的值 **@publisher_security_mode** ，以及 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] @publisher_login **@publisher_login** @job_login **@publisher_password**。 這麼做會為發行集建立快照集代理程式作業。  
  
5.  (選擇性) 更新 [sp_addarticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) 的執行，以針對實作新複寫功能的參數設定預設以外的值。  
  
### <a name="to-upgrade-scripts-that-add-subscriptions-to-a-snapshot-or-transactional-publication"></a>若要升級將訂閱加入至快照式或交易式發行集的指令碼  
  
1.  在執行建立訂閱的預存程序之後，請務必執行建立「散發代理程式」作業的預存程序，以同步處理訂閱。 您使用的預存程序將依照訂閱類型而定。  
  
    -   如果是提取訂閱，則請更新 [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md) 的執行，以提供 Windows 認證，在訂閱者端執行的散發代理程式會將該認證用於 **@job_name** 和 **@job_password**。 此項作業會在執行 [sp_addpullsubscription](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)之後完成。 如需詳細資訊，請參閱 [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md)。  
  
    -   如果是發送訂閱，請在發行者端執行 [sp_addpushsubscription_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md)。 指定 **@subscriber**、 **@subscriber_db**、 **@publication**、「Windows 認證」等 (在「散發者」端執行的「散發代理程式」會將該認證用於 **@job_name** @job_login **@job_password**)，以及此代理程式作業的排程。 如需詳細資訊，請參閱 [Specify Synchronization Schedules](../../../relational-databases/replication/specify-synchronization-schedules.md)。 此項作業會在執行 [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)之後完成。 如需詳細資訊，請參閱 [Create a Push Subscription](../../../relational-databases/replication/create-a-push-subscription.md)。  
  
### <a name="to-upgrade-scripts-that-configure-a-merge-publication"></a>若要升級設定合併式發行集的指令碼  
  
1.  (選擇性) 在現有的指令碼中，更新 [sp_addmergepublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) 的執行，以針對實作新複寫功能的參數設定預設以外的值。  
  
2.  在 [sp_addmergepublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) 之後，於發行集資料庫的發行者端執行 [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)。 指定 **@publication** 和「Windows 認證」，「快照集代理程式」執行時會將該認證用於 **@job_name** @job_login **@job_password**。 如果代理程式會在與「發行者」時連接時使用「 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證」，則也必須指定 **@publisher_security_mode** 的值 **@publisher_security_mode** ，以及 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] @publisher_login **@publisher_login** @job_login **@publisher_password**。 這麼做會為發行集建立快照集代理程式作業。  
  
3.  (選擇性) 更新 [sp_addmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) 的執行，以針對實作新複寫功能的參數設定預設以外的值。  
  
### <a name="to-upgrade-scripts-that-add-subscriptions-to-a-merge-publication"></a>若要升級將訂閱加入至合併式發行集的指令碼  
  
1.  在執行建立訂閱的預存程序之後，請務必執行建立「合併代理程式」作業的預存程序，以同步處理訂閱。 您使用的預存程序將依照訂閱類型而定。  
  
    -   如果是提取訂閱，則請更新 [sp_addmergepullsubscription_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md) 的執行，以提供 Windows 認證，在訂閱者端執行的合併代理程式會將該認證用於 **@job_name** 和 **@job_password**。 此項作業會在執行 [sp_addmergepullsubscription](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)之後完成。 如需詳細資訊，請參閱 [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md)。  
  
    -   如果是發送訂閱，請在發行者端執行 [sp_addmergepushsubscription_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md)。 指定 **@subscriber**、 **@subscriber_db**、 **@publication**、「Windows 認證」等 (在「散發者」端執行的「合併代理程式」會將該認證用於 **@job_name** @job_login **@job_password**)，以及此代理程式作業的排程。 如需詳細資訊，請參閱 [Specify Synchronization Schedules](../../../relational-databases/replication/specify-synchronization-schedules.md)。 此項作業會在執行 [sp_addmergesubscription](../../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)之後完成。 如需詳細資訊，請參閱 [Create a Push Subscription](../../../relational-databases/replication/create-a-push-subscription.md)。  
  
## <a name="example"></a>範例  
 下列的 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 指令碼範例會針對 Product 資料表建立交易式發行集。 此發行集支援立即更新，且使用佇列更新做為容錯移轉。 為了利於閱讀，已經移除了預設的參數。  
  
 [!code-sql[HowTo#sp_createtranpub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_1.sql)]  
  
## <a name="example"></a>範例  
 下列是前述指令碼的升級範例 (此指令碼會建立交易式發行集)，能成功地執行於 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 和更新版本。 此發行集支援立即更新，且使用佇列更新做為容錯移轉。 已明確地宣告新參數的預設值。  
  
> [!NOTE]  
>  Windows 認證是在執行階段使用 **sqlcmd** 指令碼變數提供的。  
  
 [!code-sql[HowTo#sp_createtranpub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_2.sql)]  
  
## <a name="example"></a>範例  
 下列的 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 指令碼範例會針對 Customers 資料表建立合併式發行集。 為了利於閱讀，已經移除了預設的參數。  
  
 [!code-sql[HowTo#sp_createmergepub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_3.sql)]  
  
## <a name="example"></a>範例  
 下列是前述指令碼的升級範例 (此指令碼會建立合併式發行集)，能成功地執行於 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 和更新版本。 已明確地宣告新參數的預設值。  
  
> [!NOTE]  
>  Windows 認證是在執行階段使用 **sqlcmd** 指令碼變數提供的。  
  
 [!code-sql[HowTo#sp_createmergepub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_4.sql)]  
  
## <a name="example"></a>範例  
 下列的 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 指令碼範例會建立交易式發行集的發送訂閱。 為了利於閱讀，已經移除了預設的參數。  
  
 [!code-sql[HowTo#sp_createtranpushsub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_5.sql)]  
  
## <a name="example"></a>範例  
 下列是前述指令碼的升級範例 (此指令碼會建立交易式發行集的發送訂閱)，能成功地執行於 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 和更新版本。 已明確地宣告新參數的預設值。  
  
> [!NOTE]  
>  Windows 認證是在執行階段使用 **sqlcmd** 指令碼變數提供的。  
  
 [!code-sql[HowTo#sp_createtranpushsub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_6.sql)]  
  
## <a name="example"></a>範例  
 下列的 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 指令碼範例會建立合併式發行集的發送訂閱。 為了利於閱讀，已經移除了預設的參數。  
  
 [!code-sql[HowTo#sp_createmergepushsub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_7.sql)]  
  
## <a name="example"></a>範例  
 下列是前述指令碼的升級範例 (此指令碼會建立合併式發行集的發送訂閱)，能成功地執行於 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 和更新版本。 已明確地宣告新參數的預設值。  
  
> [!NOTE]  
>  Windows 認證是在執行階段使用 **sqlcmd** 指令碼變數提供的。  
  
 [!code-sql[HowTo#sp_createmergepushsub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_8.sql)]  
  
## <a name="example"></a>範例  
 下列的 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 指令碼範例會建立交易式發行集的提取訂閱。 為了利於閱讀，已經移除了預設的參數。  
  
 [!code-sql[HowTo#sp_createmergepushsub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_7.sql)]  
  
## <a name="example"></a>範例  
 下列是前述指令碼的升級範例 (此指令碼會建立交易式發行集的提取訂閱)，能成功地執行於 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 和更新版本。 已明確地宣告新參數的預設值。  
  
> [!NOTE]  
>  Windows 認證是在執行階段使用 **sqlcmd** 指令碼變數提供的。  
  
 [!code-sql[HowTo#sp_createtranpullsub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_9.sql)]  
  
## <a name="example"></a>範例  
 下列的 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 指令碼範例會建立合併式發行集的提取訂閱。 為了利於閱讀，已經移除了預設的參數。  
  
 [!code-sql[HowTo#sp_createmergepullsub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_10.sql)]  
  
## <a name="example"></a>範例  
 下列是前述指令碼的升級範例 (此指令碼會建立合併式發行集的提取訂閱)，能成功地執行於 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 和更新版本。 已明確地宣告新參數的預設值。  
  
> [!NOTE]  
>  Windows 認證是在執行階段使用 **sqlcmd** 指令碼變數提供的。  
  
 [!code-sql[HowTo#sp_createmergepullsub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_11.sql)]  
  
## <a name="see-also"></a>另請參閱  
 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)   
 [Create a Push Subscription](../../../relational-databases/replication/create-a-push-subscription.md)   
 [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md)   
 [檢視及修改複寫安全性設定](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [MSSQL_ENG021797](../../../relational-databases/replication/mssql-eng021797.md)   
 [MSSQL_ENG021798](../../../relational-databases/replication/mssql-eng021798.md)   
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [升級複寫的資料庫](../../../database-engine/install-windows/upgrade-replicated-databases.md)  
  
  
