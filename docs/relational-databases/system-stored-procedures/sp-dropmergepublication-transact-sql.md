---
title: sp_dropmergepublication & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_dropmergepublication
- sp_dropmergepublication_TSQL
helpviewer_keywords:
- sp_dropmergepublication
ms.assetid: 9e1cb96e-5889-4f97-88cd-f60cf313ce68
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8876bc0e1007d942bde42a9a5a2472b58f6fa1f5
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43030786"
---
# <a name="spdropmergepublication-transact-sql"></a>sp_dropmergepublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 [ **@publication=**] **'***publication***'**  
 這是要卸除的發行集名稱。 *發行集*已**sysname**，沒有預設值。 如果**所有**，移除所有現有的合併式發行集以及與其相關聯的快照集代理程式作業。 如果您指定特定值如*發行集*，會卸除這個發行集和其相關聯的快照集代理程式作業。  
  
 [  **@ignore_distributor =**] *ignore_distributor*  
 用來卸除發行集，且不在散發者端執行清除作業。 *ignore_distributor*已**位元**，預設值是**0**。 當重新安裝散發者時，也會使用這個參數。  
  
 [  **@reserved=**]*保留*  
 保留供日後使用。 *保留*已**位元**，預設值是**0**。  
  
 [  **@ignore_merge_metadata=** ] *ignore_merge_metadata*  
 僅供內部使用。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_dropmergepublication**用於合併式複寫中。  
  
 **sp_dropmergepublication**遞迴卸除發行集相關聯的所有發行項，然後再卸除發行集本身。 如果發行集有一或多項訂閱，便不能移除它。 如需有關如何移除訂用帳戶的資訊，請參閱 < [Delete a Push Subscription](../../relational-databases/replication/delete-a-push-subscription.md)並[Delete a Pull Subscription](../../relational-databases/replication/delete-a-pull-subscription.md)。  
  
 執行**sp_dropmergepublication**卸除發行集不會移除已發行的物件從發行集資料庫或從訂閱資料庫對應的物件。 請使用 DROP\<物件 > 來手動移除這些物件，如有必要。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_dropmergepublication](../../relational-databases/replication/codesnippet/tsql/sp-dropmergepublication-_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_dropmergepublication**。  
  
## <a name="see-also"></a>另請參閱  
 [刪除發行集](../../relational-databases/replication/publish/delete-a-publication.md)   
 [sp_addmergepublication &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)   
 [sp_changemergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)   
 [sp_helpmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
