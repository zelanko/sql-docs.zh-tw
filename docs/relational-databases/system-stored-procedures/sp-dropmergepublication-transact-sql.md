---
title: sp_dropmergepublication （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropmergepublication
- sp_dropmergepublication_TSQL
helpviewer_keywords:
- sp_dropmergepublication
ms.assetid: 9e1cb96e-5889-4f97-88cd-f60cf313ce68
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e9b2b36484d34396ed573f4b06bd1feb5b0f83b1
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85881835"
---
# <a name="sp_dropmergepublication-transact-sql"></a>sp_dropmergepublication (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  卸除合併式發行集及其相關快照集代理程式。 在卸除合併式發行集之前，必須先卸除所有訂閱。 發行集中的發行項會自動卸除。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_dropmergepublication [ @publication= ] 'publication'   
    [ , [ @ignore_distributor = ] ignore_distributor ]   
    [ , [ @reserved = ] reserved ]  
    [ , [ @ignore_merge_metadata = ] ignore_merge_metadata ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'`這是要卸載的發行集名稱。 *發行*集是**sysname**，沒有預設值。 如果是**all**，就會移除所有現有的合併式發行集，以及與它們相關聯的快照集代理程式作業。 如果您指定*發行*集的特定值，則只會卸載該發行集及其相關聯的快照集代理程式作業。  
  
`[ @ignore_distributor = ] ignore_distributor`用來卸載發行集，而不在散發者上執行清除工作。 *ignore_distributor*是**bit**，預設值是**0**。 當重新安裝散發者時，也會使用這個參數。  
  
`[ @reserved = ] reserved`保留供日後使用。 *reserved*是**bit**，預設值是**0**。  
  
`[ @ignore_merge_metadata = ] ignore_merge_metadata`僅供內部使用。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_dropmergepublication**用於合併式複寫中。  
  
 **sp_dropmergepublication**會以遞迴方式卸載與發行集相關聯的所有文章，然後卸載發行集本身。 如果發行集有一或多項訂閱，便不能移除它。 如需如何移除訂閱的詳細資訊，請參閱[刪除發送訂閱](../../relational-databases/replication/delete-a-push-subscription.md)和[刪除提取訂閱](../../relational-databases/replication/delete-a-pull-subscription.md)。  
  
 執行**sp_dropmergepublication**來卸載發行集並不會從發行集資料庫中移除發行的物件，也不會從訂閱資料庫中移除對應的物件。 如有需要，請使用 DROP \<object> 來手動移除這些物件。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_dropmergepublication](../../relational-databases/replication/codesnippet/tsql/sp-dropmergepublication-_1.sql)]  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色或**db_owner**固定資料庫角色的成員，才能夠執行**sp_dropmergepublication**。  
  
## <a name="see-also"></a>另請參閱  
 [刪除發行集](../../relational-databases/replication/publish/delete-a-publication.md)   
 [sp_addmergepublication &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)   
 [sp_changemergepublication &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)   
 [sp_helpmergepublication &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
