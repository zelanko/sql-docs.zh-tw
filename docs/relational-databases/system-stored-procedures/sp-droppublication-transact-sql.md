---
title: sp_droppublication （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_droppublication_TSQL
- sp_droppublication
helpviewer_keywords:
- sp_droppublication
ms.assetid: b52b37e6-4fec-40cf-abba-7dce4ff395fd
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 3ef56f46696a2cb145804105d4d5f22fded6fe1f
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82829999"
---
# <a name="sp_droppublication-transact-sql"></a>sp_droppublication (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  卸除發行集及其相關快照集代理程式。 在卸除發行集之前，必須先卸除所有訂閱。 發行集中的發行項會自動卸除。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_droppublication [ @publication= ] 'publication'   
    [ , [ @ignore_distributor = ] ignore_distributor ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'`這是要卸載的發行集名稱。 *發行*集是**sysname**，沒有預設值。 如果指定**all** ，則除了具有訂閱的發行集之外，所有發行集都會從發行集資料庫中卸載。  
  
`[ @ignore_distributor = ] ignore_distributor` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_droppublication**用於快照式複寫和異動複寫中。  
  
 **sp_droppublication**會以遞迴方式卸載與發行集相關聯的所有文章，然後卸載發行集本身。 如果發行集有一或多項訂閱，便不能移除它。 如需如何移除訂閱的詳細資訊，請參閱[刪除發送訂閱](../../relational-databases/replication/delete-a-push-subscription.md)和[刪除提取訂閱](../../relational-databases/replication/delete-a-pull-subscription.md)。  
  
 執行**sp_droppublication**來卸載發行集並不會從發行集資料庫中移除發行的物件，也不會從訂閱資料庫中移除對應的物件。 \<如有必要，請使用 DROP object> 以手動方式移除這些物件。  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色的成員，才能夠執行**sp_droppublication**。  
  
## <a name="examples"></a>範例  
 [!code-sql[HowTo#sp_droppublication](../../relational-databases/replication/codesnippet/tsql/sp-droppublication-trans_1.sql)]  
  
## <a name="see-also"></a>另請參閱  
 [刪除發行集](../../relational-databases/replication/publish/delete-a-publication.md)   
 [sp_addpublication &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_changepublication &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [sp_helppublication &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
