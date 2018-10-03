---
title: sp_reinitmergepullsubscription & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_reinitmergepullsubscription
- sp_reinitmergepullsubscription_TSQL
helpviewer_keywords:
- sp_reinitmergepullsubscription
ms.assetid: 48464bc9-60aa-4886-b526-163f010102b8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e1f826b48896dda673dc7d34dd13357e169961f4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47756526"
---
# <a name="spreinitmergepullsubscription-transact-sql"></a>sp_reinitmergepullsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  將合併提取訂閱標示為在下次執行合併代理程式時重新初始化。 這個預存程序執行於訂閱資料庫的訂閱者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_reinitmergepullsubscription [ [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publisher_db' ]  
    [ , [ @publication = ] 'publication' ]  
    [ , [ @upload_first = ] 'upload_first'  
```  
  
## <a name="arguments"></a>引數  
 [ **@publisher** = ] **'***publisher***'**  
 這是發行者的名稱。 *發行者*已**sysname**，所有的預設值。  
  
 [ **@publisher_db** = ] **'***publisher_db***'**  
 這是發行者資料庫的名稱。 *publisher_db*已**sysname**，所有的預設值。  
  
 [ **@publication** = ] **'***publication***'**  
 這是發行集的名稱。 *發行集*已**sysname**，所有的預設值。  
  
 [ **@upload_first** =] **'***upload_first***'**  
 這是指在訂閱重新初始化之前，是否上傳在訂閱者端的變更。 *upload_first*已**nvarchar(5)**，預設值是 FALSE。 如果 **，則為 true**，訂用帳戶重新初始化之前上傳變更。 如果**false**，不會上傳變更。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_reinitmergepullsubscription**用於合併式複寫中。  
  
 如果您新增、卸除或變更參數化篩選，在重新初始化期間，便無法將訂閱者的暫止變更上傳到發行者。 如果您要上傳暫止變更，請在變更篩選之前，同步處理所有訂閱。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_reinitmergepullsub](../../relational-databases/replication/codesnippet/tsql/sp-reinitmergepullsubscr_1.sql)]  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_reinitmergepullsubwithupload](../../relational-databases/replication/codesnippet/tsql/sp-reinitmergepullsubscr_2.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_reinitmergepullsubscription**。  
  
## <a name="see-also"></a>另請參閱  
 [重新初始化訂閱](../../relational-databases/replication/reinitialize-a-subscription.md)   
 [重新初始化訂閱](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
