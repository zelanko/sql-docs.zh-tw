---
title: sp_mergecleanupmetadata (TRANSACT-SQL) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 6924ef36c57036cf6cad6e25a6dc5cebfa5fa5f2
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58529000"
---
# <a name="spmergecleanupmetadata-transact-sql"></a>sp_mergecleanupmetadata (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  應該只能用在所包含的伺服器執行版本的複寫拓撲[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之前[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]Service Pack 1。**sp_mergecleanupmetadata**可讓管理員清除中繼資料**MSmerge_genhistory**， **MSmerge_contents**和**MSmerge_tombstone**系統資料表。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_mergecleanupmetadata [ [ @publication = ] 'publication' ]  
    [ , [ @reinitialize_subscriber = ] 'reinitialize_subscriber' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'` 是發行集名稱。 *發行集*已**sysname**，預設值是**%**，會清除所有發行集的中繼資料。 如果明確指定的話，發行集必須已存在。  
  
`[ @reinitialize_subscriber = ] 'subscriber'` 指定是否要重新初始化訂閱者。 *訂閱者*是**nvarchar(5)**，可以是**TRUE**或**FALSE**，預設值是**TRUE**。 如果 **，則為 TRUE**，訂用帳戶會標示重新初始化。 如果**FALSE**，訂用帳戶未標示為重新初始化。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_mergecleanupmetadata**應該只能用在所包含的伺服器執行版本的複寫拓撲[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之前[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]Service Pack 1。 只包含 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 1 或更新版本的拓撲，應該使用以自動保留為基礎的中繼資料清除功能。 當執行這個預存程序時，請注意，執行這個預存程序的電腦之記錄檔必然會成長，且可能會大幅成長。  
  
> [!CAUTION]
>  在後**sp_mergecleanupmetadata**執行時，根據預設，所有訂用帳戶在訂閱者端的發行集的中繼資料儲存在**MSmerge_genhistory**， **MSmerge_contents**並**MSmerge_tombstone**會標示為重新初始化，訂閱者的任何暫止的變更都會遺失，和目前的快照集已標記為過時。  
> 
> [!NOTE]
>  如果有多個發行集資料庫上，且任何一個發行集都會使用無限期的發行保留期限 (**@retention**=**0**)、 執行**sp_mergecleanupmetadata**就不會清除追蹤資料庫中繼資料的合併式複寫變更。 因此，在使用無限期的發行期限時，一定要特別小心。  
  
 當執行這個預存程序時，您可以選擇是否要重新初始化訂閱者，藉由設定**@reinitialize_subscriber**參數來**TRUE** （預設值） 或**FALSE**. 如果**sp_mergecleanupmetadata**執行**@reinitialize_subscriber**參數設為**TRUE**，快照集也會重新套用在訂閱者即使訂用帳戶建立沒有初始快照集 （例如，如果快照集資料和結構描述已手動套用，或已存在於訂閱者）。 將參數設定為**FALSE**應小心，因為如果不會重新初始化發行集，您必須確定在發行者和訂閱者的資料會同步處理。  
  
 值為何**@reinitialize_subscriber**， **sp_mergecleanupmetadata**失敗，如果有進行中合併正要將變更上傳到 「 發行者 」 或在重新發行訂閱者的程序預存程序會叫用的時間。  
  
 **執行與 sp_mergecleanupmetadata @reinitialize_subscriber = TRUE:**  
  
1.  建議您停止發行集和訂閱資料庫的所有更新，但您不一定需要如此。 如果繼續更新，當發行集重新初始化時，您將失去自上次合併之後，在訂閱者端進行的任何更新，但仍會維護資料的聚合。  
  
2.  執行合併代理程式來執行合併。 我們建議您改用 **-驗證**代理程式命令列選項，當您執行 「 合併代理程式時，每個訂閱者端。 如果您在執行連續模式合併，請參閱*連續模式合併的特殊考量*本主題稍後的。  
  
3.  所有合併都完成之後，請執行**sp_mergecleanupmetadata**。  
  
4.  執行**sp_reinitmergepullsubscription**上所有的訂閱者使用具名或匿名提取訂閱，以確保資料聚合。  
  
5.  如果您在執行連續模式合併，請參閱*連續模式合併的特殊考量*本主題稍後的。  
  
6.  重新產生所有層級所涉及之所有合併式發行集的快照集檔案。 如果您試圖在尚未重新產生快照集前進行合併，系統會提示您重新產生快照集。  
  
7.  備份發行集資料庫。 如果沒有完成這個動作，在還原發行集資料庫之後，合併可能會失敗。  
  
 **執行與 sp_mergecleanupmetadata @reinitialize_subscriber = FALSE:**  
  
1.  停止**所有**發行集和訂閱資料庫的更新。  
  
2.  執行合併代理程式來執行合併。 我們建議您改用 **-驗證**代理程式命令列選項，當您執行 「 合併代理程式時，每個訂閱者端。 如果您在執行連續模式合併，請參閱*連續模式合併的特殊考量*本主題稍後的。  
  
3.  所有合併都完成之後，請執行**sp_mergecleanupmetadata**。  
  
4.  如果您在執行連續模式合併，請參閱*連續模式合併的特殊考量*本主題稍後的。  
  
5.  重新產生所有層級所涉及之所有合併式發行集的快照集檔案。 如果您試圖在尚未重新產生快照集前進行合併，系統會提示您重新產生快照集。  
  
6.  備份發行集資料庫。 如果沒有完成這個動作，在還原發行集資料庫之後，合併可能會失敗。  
  
 **連續模式合併的特殊考量**  
  
 如果您在執行連續模式的合併，您必須執行下列動作之一：  
  
-   停止合併代理程式，然後再執行另一個合併，但不 **-連續**指定的參數。  
  
-   停用發行集中**sp_changemergepublication** ，確保任何輪詢發行集狀態的連續模式合併會失敗。  
  
    ```  
    EXEC central..sp_changemergepublication @publication = 'dynpart_pubn', @property = 'status', @value = 'inactive'  
    ```  
  
 當您完成的步驟 3 中執行**sp_mergecleanupmetadata**，根據您對它們所做的停止連續模式合併的繼續。 您可以執行下列動作之一：  
  
-   新增 **-連續**回 「 合併代理程式參數。  
  
-   重新啟動發行集中**sp_changemergepublication。**  
  
    ```  
    EXEC central..sp_changemergepublication @publication = 'dynpart_pubn', @property = 'status', @value = 'active'  
    ```  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_mergecleanupmetadata**。  
  
 若要使用這個預存程序，發行者必須執行 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]。 訂閱者必須執行[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]或是[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 Service Pack 2。  
  
## <a name="see-also"></a>另請參閱  
 [MSmerge_genhistory &#40;Transact-SQL&#41;](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md)   
 [MSmerge_contents &#40;Transact-SQL&#41;](../../relational-databases/system-tables/msmerge-contents-transact-sql.md)   
 [MSmerge_tombstone &#40;Transact-SQL&#41;](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md)  
  
  
