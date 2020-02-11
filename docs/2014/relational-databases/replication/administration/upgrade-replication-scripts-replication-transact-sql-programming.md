---
title: 升級複寫指令碼 (複寫 Transact-SQL 程式設計) | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- scripts [SQL Server replication], upgrading
- upgrading SQL Server, replicated databases
- upgrading replication applications
- replication [SQL Server], scripting
- replication [SQL Server], upgrading
- upgrading replicated databases
ms.assetid: 0b8720bd-f339-4842-bc8f-b35a46f6d3ee
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cd3f6498cbfb4ef8cf38e27879d619472a6693ce
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68210768"
---
# <a name="upgrade-replication-scripts-replication-transact-sql-programming"></a>升級複寫指令碼 (複寫 Transact-SQL 程式設計)
  [!INCLUDE[tsql](../../../includes/tsql-md.md)] 指令碼檔案可以用於以程式設計的方式設定複寫拓撲。 如需詳細資訊，請參閱[複寫系統預存程序概念](../concepts/replication-system-stored-procedures-concepts.md)。  
  
> [!IMPORTANT]  
>  雖然並不一定要升級由 `sysadmin` 角色的成員所執行的指令碼，但建議您依照本主題所述修改現有的指令碼。 請根據主題＜ [Replication Agent Security Model](../security/replication-agent-security-model.md)＞的「代理程式所需的權限」一節所述，為每個複寫代理程式指定具有最小權限的帳戶。  
  
 這些安全性改進會影響現有指令碼中的下列預存程序，讓您可以明確地指定 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 帳戶，並在這些帳戶下執行複寫代理程式工作，對權限可以有更多的控制：  
  
-   **sp_addpublication_snapshot**:  
  
     您現在應該提供 Windows 認證做為**@job_login** ， **@job_password**並在執行[sp_addpublication_snapshot &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql) ，以建立快照集代理程式在散發者端執行時所用的作業。  
  
-   **sp_addpushsubscription_agent**：  
  
     您現在應該執行[sp_addpushsubscription_agent &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql)以明確地加入作業，並提供在「散發者」**@job_login**端**@job_password**執行散發代理程式作業的 Windows 認證（和）。 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]版本中，這項作業會在建立發送訂閱時自動完成。  
  
-   **sp_addmergepushsubscription_agent**：  
  
     您現在應該執行[sp_addmergepushsubscription_agent &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql)以明確地加入作業，並提供在「散發者」**@job_login**端**@job_password**執行合併代理程式作業的 Windows 認證（和）。 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]版本中，這項作業會在建立發送訂閱時自動完成。  
  
-   **sp_addpullsubscription_agent**：  
  
     您現在應該提供 Windows 認證做為**@job_login** ， **@job_password**並在執行[sp_addpullsubscription_agent &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql) ，以建立在訂閱者端執行散發代理程式的作業。  
  
-   **sp_addmergepullsubscription_agent**：  
  
     您現在應該提供 Windows 認證做為**@job_login** ， **@job_password**並在執行[sp_addmergepullsubscription_agent &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql) ，以建立在訂閱者端執行合併代理程式的作業。  
  
-   **sp_addlogreader_agent**：  
  
     現在應該執行 [sp_addlogreader_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql) 以手動新增作業並提供 Windows 認證，藉此在散發者端執行記錄讀取器代理程式。 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]版本中，這項作業會在建立交易式發行集時自動完成。  
  
-   **sp_addqreader_agent**：  
  
     現在應該執行 [sp_addqreader_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql) 以手動新增作業並提供 Windows 認證，藉此在散發者端執行佇列讀取器代理程式。 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]版本中，這項作業會在建立支援佇列更新的交易式發行集時自動完成。  
  
 在[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]中導入的安全性模型中，複寫代理程式一律會使用和[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **@job_name** **@job_password**中提供的認證，透過 Windows 驗證連接到的本機實例。 如需有關在執行複寫代理程式作業時所使用 Windows 帳戶之需求的資訊，請參閱＜ [Replication Agent Security Model](../security/replication-agent-security-model.md)＞。  
  
> [!IMPORTANT]  
>  可能的話，會在執行階段提示使用者輸入安全性認證。 如果將認證儲存在指令碼檔案中，請確定該檔案本身受到安全保護。  
  
### <a name="to-upgrade-scripts-that-configure-a-snapshot-or-transactional-publication"></a>若要升級設定快照式或交易式發行集的指令碼  
  
1.  在現有指令碼的 [sp_addpublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql) 之前，於發行集資料庫的發行者端執行 [sp_addlogreader_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql)。 指定用來**@job_name**執行和**@job_password**之記錄讀取器代理程式的 Windows 認證。 如果代理程式在連接[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]到發行者時將使用驗證，您也必須為**@publisher_security_mode**指定**0**的值，並針對[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **@publisher_login**和**@publisher_password**指定登入資訊。 如此會建立發行集資料庫的「記錄讀取器代理程式」作業。  
  
    > [!NOTE]  
    >  只有交易式發行集才需要這個步驟，快照式發行集不需要。  
  
2.  (選擇性) 在 [sp_addpublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql) 之前，於散發資料庫的散發者端執行 [sp_addqreader_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql)。 指定用來**@job_name**執行和**@job_password**之佇列讀取器代理程式的 Windows 認證。 如此會為「散發者」建立「佇列讀取器代理程式」作業。  
  
    > [!NOTE]  
    >  只有支援佇列更新訂閱者的交易式發行集才需要這個步驟。  
  
3.  (選擇性) 更新 [sp_addpublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql) 的執行，以針對實作新複寫功能的參數設定預設以外的值。  
  
4.  在 [sp_addpublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql) 之後，於發行集資料庫的發行者端執行 [sp_addpublication_snapshot &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql)。 指定**@publication**和用來執行**@job_name**和**@job_password**之快照集代理程式的 Windows 認證。 如果代理程式在連接[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]到發行者時將使用驗證，您也必須為**@publisher_security_mode**指定**0**的值，並針對[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **@publisher_login**和**@publisher_password**指定登入資訊。 這麼做會為發行集建立快照集代理程式作業。  
  
5.  (選擇性) 更新 [sp_addarticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql) 的執行，以針對實作新複寫功能的參數設定預設以外的值。  
  
### <a name="to-upgrade-scripts-that-add-subscriptions-to-a-snapshot-or-transactional-publication"></a>若要升級將訂閱加入至快照式或交易式發行集的指令碼  
  
1.  在執行建立訂閱的預存程序之後，請務必執行建立「散發代理程式」作業的預存程序，以同步處理訂閱。 您使用的預存程序將依照訂閱類型而定。  
  
    -   針對提取訂閱，更新[sp_addpullsubscription_agent &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql)的執行，以提供在**@job_name**和**@job_password**的「訂閱者」端執行散發代理程式時所使用的 Windows 認證。 此項作業會在執行 [sp_addpullsubscription](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql)之後完成。 如需詳細資訊，請參閱 [建立提取訂閱](../create-a-pull-subscription.md)。  
  
    -   如果是發送訂閱，請在發行者端執行 [sp_addpushsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql)。 指定**@subscriber**、 **@subscriber_db**、 **@publication**、用來**@job_name**在和**@job_password**之散發者端執行散發代理程式的 Windows 認證，以及此代理程式作業的排程。 如需詳細資訊，請參閱 [Specify Synchronization Schedules](../specify-synchronization-schedules.md)。 此項作業會在執行 [sp_addsubscription](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql)之後完成。 如需詳細資訊，請參閱 [建立發送訂閱](../create-a-push-subscription.md)。  
  
### <a name="to-upgrade-scripts-that-configure-a-merge-publication"></a>若要升級設定合併式發行集的指令碼  
  
1.  (選擇性) 在現有的指令碼中，更新 [sp_addmergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql) 的執行，以針對實作新複寫功能的參數設定預設以外的值。  
  
2.  在 [sp_addmergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql) 之後，於發行集資料庫的發行者端執行 [sp_addpublication_snapshot &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql)。 指定**@publication**和用來執行**@job_name**和**@job_password**之快照集代理程式的 Windows 認證。 如果代理程式在連接[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]到發行者時將使用驗證，您也必須為**@publisher_security_mode**指定**0**的值，並針對[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **@publisher_login**和**@publisher_password**指定登入資訊。 這麼做會為發行集建立快照集代理程式作業。  
  
3.  (選擇性) 更新 [sp_addmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql) 的執行，以針對實作新複寫功能的參數設定預設以外的值。  
  
### <a name="to-upgrade-scripts-that-add-subscriptions-to-a-merge-publication"></a>若要升級將訂閱加入至合併式發行集的指令碼  
  
1.  在執行建立訂閱的預存程序之後，請務必執行建立「合併代理程式」作業的預存程序，以同步處理訂閱。 您使用的預存程序將依照訂閱類型而定。  
  
    -   針對提取訂閱，更新[sp_addmergepullsubscription_agent &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql)的執行，以提供在**@job_name**和**@job_password**的「訂閱者」端執行合併代理程式時所使用的 Windows 認證。 此項作業會在執行 [sp_addmergepullsubscription](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql)之後完成。 如需詳細資訊，請參閱 [建立提取訂閱](../create-a-pull-subscription.md)。  
  
    -   如果是發送訂閱，請在發行者端執行 [sp_addmergepushsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql)。 指定**@subscriber**、 **@subscriber_db**、 **@publication**、用來執行散發者之合併代理程式的**@job_name** Windows 認證**@job_password**，以及此代理程式作業的排程。 如需詳細資訊，請參閱 [Specify Synchronization Schedules](../specify-synchronization-schedules.md)。 此項作業會在執行 [sp_addmergesubscription](/sql/relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql)之後完成。 如需詳細資訊，請參閱 [建立發送訂閱](../create-a-push-subscription.md)。  
  
## <a name="example"></a>範例  
 下列的 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 指令碼範例會針對 Product 資料表建立交易式發行集。 此發行集支援立即更新，且使用佇列更新做為容錯移轉。 為了利於閱讀，已經移除了預設的參數。  
  
 [!code-sql[HowTo#sp_createtranpub_NWpreupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwtranpub80.sql#sp_createtranpub_nwpreupgrade)]  
  
## <a name="example"></a>範例  
 下列是前述指令碼的升級範例 (此指令碼會建立交易式發行集)，能成功地執行於 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 和更新版本。 此發行集支援立即更新，且使用佇列更新做為容錯移轉。 已明確地宣告新參數的預設值。  
  
> [!NOTE]  
>  Windows 認證是在執行階段使用 **sqlcmd** 指令碼變數提供的。  
  
 [!code-sql[HowTo#sp_createtranpub_NWpostupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwtranpublication.sql#sp_createtranpub_nwpostupgrade)]  
  
## <a name="example"></a>範例  
 下列的 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 指令碼範例會針對 Customers 資料表建立合併式發行集。 為了利於閱讀，已經移除了預設的參數。  
  
 [!code-sql[HowTo#sp_createmergepub_NWpreupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwmergepub80.sql#sp_createmergepub_nwpreupgrade)]  
  
## <a name="example"></a>範例  
 下列是前述指令碼的升級範例 (此指令碼會建立合併式發行集)，能成功地執行於 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 和更新版本。 已明確地宣告新參數的預設值。  
  
> [!NOTE]  
>  Windows 認證是在執行階段使用 **sqlcmd** 指令碼變數提供的。  
  
 [!code-sql[HowTo#sp_createmergepub_NWpostupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwmergepublication.sql#sp_createmergepub_nwpostupgrade)]  
  
## <a name="example"></a>範例  
 下列的 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 指令碼範例會建立交易式發行集的發送訂閱。 為了利於閱讀，已經移除了預設的參數。  
  
 [!code-sql[HowTo#sp_createtranpushsub_NWpreupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwtranpushsub80.sql#sp_createtranpushsub_nwpreupgrade)]  
  
## <a name="example"></a>範例  
 下列是前述指令碼的升級範例 (此指令碼會建立交易式發行集的發送訂閱)，能成功地執行於 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 和更新版本。 已明確地宣告新參數的預設值。  
  
> [!NOTE]  
>  Windows 認證是在執行階段使用 **sqlcmd** 指令碼變數提供的。  
  
 [!code-sql[HowTo#sp_createtranpushsub_NWpostupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwpushsub.sql#sp_createtranpushsub_nwpostupgrade)]  
  
## <a name="example"></a>範例  
 下列的 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 指令碼範例會建立合併式發行集的發送訂閱。 為了利於閱讀，已經移除了預設的參數。  
  
 [!code-sql[HowTo#sp_createmergepushsub_NWpreupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwmergepushsub80.sql#sp_createmergepushsub_nwpreupgrade)]  
  
## <a name="example"></a>範例  
 下列是前述指令碼的升級範例 (此指令碼會建立合併式發行集的發送訂閱)，能成功地執行於 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 和更新版本。 已明確地宣告新參數的預設值。  
  
> [!NOTE]  
>  Windows 認證是在執行階段使用 **sqlcmd** 指令碼變數提供的。  
  
 [!code-sql[HowTo#sp_createmergepushsub_NWpostupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwpushsub.sql#sp_createmergepushsub_nwpostupgrade)]  
  
## <a name="example"></a>範例  
 下列的 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 指令碼範例會建立交易式發行集的提取訂閱。 為了利於閱讀，已經移除了預設的參數。  
  
 [!code-sql[HowTo#sp_createmergepushsub_NWpreupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwmergepushsub80.sql#sp_createmergepushsub_nwpreupgrade)]  
  
## <a name="example"></a>範例  
 下列是前述指令碼的升級範例 (此指令碼會建立交易式發行集的提取訂閱)，能成功地執行於 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 和更新版本。 已明確地宣告新參數的預設值。  
  
> [!NOTE]  
>  Windows 認證是在執行階段使用 **sqlcmd** 指令碼變數提供的。  
  
 [!code-sql[HowTo#sp_createtranpullsub_NWpostupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwpullsub.sql#sp_createtranpullsub_nwpostupgrade)]  
  
## <a name="example"></a>範例  
 下列的 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 指令碼範例會建立合併式發行集的提取訂閱。 為了利於閱讀，已經移除了預設的參數。  
  
 [!code-sql[HowTo#sp_createmergepullsub_NWpreupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwmergepullsub80.sql#sp_createmergepullsub_nwpreupgrade)]  
  
## <a name="example"></a>範例  
 下列是前述指令碼的升級範例 (此指令碼會建立合併式發行集的提取訂閱)，能成功地執行於 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 和更新版本。 已明確地宣告新參數的預設值。  
  
> [!NOTE]  
>  Windows 認證是在執行階段使用 **sqlcmd** 指令碼變數提供的。  
  
 [!code-sql[HowTo#sp_createmergepullsub_NWpostupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwpullsub.sql#sp_createmergepullsub_nwpostupgrade)]  
  
## <a name="see-also"></a>另請參閱  
 [Create a Publication](../publish/create-a-publication.md)   
 [Create a Push Subscription](../create-a-push-subscription.md)   
 [Create a Pull Subscription](../create-a-pull-subscription.md)   
 [檢視及修改複寫安全性設定](../security/view-and-modify-replication-security-settings.md)   
 [MSSQL_ENG021797](../mssql-eng021797.md)   
 [MSSQL_ENG021798](../mssql-eng021798.md)   
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)   
 [升級複寫的資料庫](../../../database-engine/install-windows/upgrade-replicated-databases.md)  
  
  
