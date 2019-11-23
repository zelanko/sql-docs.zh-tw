---
title: sp_mergecleanupmetadata （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_mergecleanupmetadata_TSQL
- sp_mergecleanupmetadata
helpviewer_keywords:
- sp_mergecleanupmetadata
ms.assetid: 892f8628-4cbe-4cc3-b959-ed45ffc24064
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0196993f863d973e14834f7eb3b93b797a825ac4
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/25/2019
ms.locfileid: "72907329"
---
# <a name="sp_mergecleanupmetadata-transact-sql"></a>sp_mergecleanupmetadata (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  應該僅用於包含執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 1 之前版本 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 之伺服器的複寫拓撲。**sp_mergecleanupmetadata**可讓系統管理員清除**MSmerge_genhistory**、 **MSmerge_contents**和**MSmerge_tombstone**系統資料表中的中繼資料。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_mergecleanupmetadata [ [ @publication = ] 'publication' ]  
    [ , [ @reinitialize_subscriber = ] 'reinitialize_subscriber' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'` 是發行集的名稱。 *發行*集是**sysname**，預設值是 **%** ，這會清除所有發行集的中繼資料。 如果明確指定的話，發行集必須已存在。  
  
`[ @reinitialize_subscriber = ] 'subscriber'` 指定是否要重新初始化訂閱者。 *訂閱者*是**Nvarchar （5）** ，可以是**true**或**FALSE**，預設值是**true**。 若**為 TRUE**，則會將訂閱標示為重新初始化。 若為**FALSE**，則不會將訂閱標示為重新初始化。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>Remarks  
 **sp_mergecleanupmetadata**只能用在包含 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 1 之前執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本之伺服器的複寫拓撲中。 只包含 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 1 或更新版本的拓撲，應該使用以自動保留為基礎的中繼資料清除功能。 當執行這個預存程序時，請注意，執行這個預存程序的電腦之記錄檔必然會成長，且可能會大幅成長。  
  
> [!CAUTION]
>  執行**sp_mergecleanupmetadata**之後，根據預設，在發行集的訂閱者上，所有具有儲存于**MSmerge_genhistory**、 **MSmerge_contents**和**MSmerge_tombstone**之中繼資料的訂閱都會標示為重新初始化，訂閱者端的任何暫止變更都會遺失，而目前的快照集會被標示為過時。  
> 
> [!NOTE]
>  如果資料庫上有多個發行集，而且其中任何一個發行集都使用無限的發行集保留期限（ **\@保留**=**0**），則執行**sp_mergecleanupmetadata**並不會清除資料庫的合併式複寫變更追蹤中繼資料。 因此，在使用無限期的發行期限時，一定要特別小心。  
  
 執行此預存程式時，您可以將 **\@reinitialize_subscriber**參數設定為**TRUE** （預設值）或**FALSE**，以選擇是否要重新初始化訂閱者。 如果**sp_mergecleanupmetadata**是以 **\@reinitialize_subscriber**參數設為**TRUE**來執行，則即使訂閱是在沒有初始快照集的情況下建立的，也會在訂閱者端重新套用快照集（例如，如果快照集資料和架構已手動套用，或已存在於訂閱者端）。 將參數設定為**FALSE**應謹慎使用，因為如果發行集不是重新初始化，您必須確定「發行者」和「訂閱者」端的資料已同步處理。  
  
 無論 **\@reinitialize_subscriber**的值為何，如果在叫用預存程式時，正在嘗試將變更上傳至發行者或重新發行訂閱者，則**sp_mergecleanupmetadata**會失敗。  
  
 **使用 \@reinitialize_subscriber = TRUE 來執行 sp_mergecleanupmetadata：**  
  
1.  建議您停止發行集和訂閱資料庫的所有更新，但您不一定需要如此。 如果繼續更新，當發行集重新初始化時，您將失去自上次合併之後，在訂閱者端進行的任何更新，但仍會維護資料的聚合。  
  
2.  執行合併代理程式來執行合併。 當您執行合併代理程式時，建議您在每個「訂閱者」**端使用-Validate**代理程式命令列選項。 如果您正在執行連續模式合併，請參閱本節稍後*的連續模式合併的特殊考慮*。  
  
3.  完成所有合併之後，請執行**sp_mergecleanupmetadata**。  
  
4.  在所有使用命名或匿名提取訂閱的訂閱者上執行**sp_reinitmergepullsubscription** ，以確保資料的聚合。  
  
5.  如果您正在執行連續模式合併，請參閱本節稍後*的連續模式合併的特殊考慮*。  
  
6.  重新產生所有層級所涉及之所有合併式發行集的快照集檔案。 如果您試圖在尚未重新產生快照集前進行合併，系統會提示您重新產生快照集。  
  
7.  備份發行集資料庫。 如果沒有完成這個動作，在還原發行集資料庫之後，合併可能會失敗。  
  
 **使用 \@reinitialize_subscriber = FALSE 執行 sp_mergecleanupmetadata：**  
  
1.  停止發行集和訂閱資料庫的**所有**更新。  
  
2.  執行合併代理程式來執行合併。 當您執行合併代理程式時，建議您在每個「訂閱者」**端使用-Validate**代理程式命令列選項。 如果您正在執行連續模式合併，請參閱本節稍後*的連續模式合併的特殊考慮*。  
  
3.  完成所有合併之後，請執行**sp_mergecleanupmetadata**。  
  
4.  如果您正在執行連續模式合併，請參閱本節稍後*的連續模式合併的特殊考慮*。  
  
5.  重新產生所有層級所涉及之所有合併式發行集的快照集檔案。 如果您試圖在尚未重新產生快照集前進行合併，系統會提示您重新產生快照集。  
  
6.  備份發行集資料庫。 如果沒有完成這個動作，在還原發行集資料庫之後，合併可能會失敗。  

 **連續模式合併的特殊考慮**  
  
 如果您在執行連續模式的合併，您必須執行下列動作之一：  
  
-   停止合併代理程式，然後執行另一個合併，但不指定 **-連續**參數。  
  
-   使用**sp_changemergepublication**停用發行集，以確保輪詢發行集狀態的任何連續模式合併都會失敗。  
  
    ```  
    EXEC central..sp_changemergepublication @publication = 'dynpart_pubn', @property = 'status', @value = 'inactive'  
    ```  
  
 當您完成執行**sp_mergecleanupmetadata**的步驟3時，請根據您停止的方式繼續連續模式合併。 您可以執行下列動作之一：  
  
-   為合併代理程式新增 **-連續**參數。  
  
-   使用 sp_changemergepublication 重新開機發行集 **。**  
  
    ```  
    EXEC central..sp_changemergepublication @publication = 'dynpart_pubn', @property = 'status', @value = 'active'  
    ```  
  
## <a name="permissions"></a>Permissions  
 只有**系統管理員（sysadmin** ）固定伺服器角色或**db_owner**固定資料庫角色的成員，才能夠執行**sp_mergecleanupmetadata**。  
  
 若要使用這個預存程序，發行者必須執行 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]。 訂閱者必須執行 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 Service Pack 2。  
  
## <a name="see-also"></a>另請參閱  
 [MSmerge_genhistory &#40;transact-sql&#41; ](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md)   
 [MSmerge_contents &#40;transact-sql&#41; ](../../relational-databases/system-tables/msmerge-contents-transact-sql.md)   
 [MSmerge_tombstone &#40;transact-sql&#41;](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md)  
  
  
