---
title: "sp_reinitmergepullsubscription (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_reinitmergepullsubscription
- sp_reinitmergepullsubscription_TSQL
helpviewer_keywords:
- sp_reinitmergepullsubscription
ms.assetid: 48464bc9-60aa-4886-b526-163f010102b8
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5d6f906cf3335079618629c03cc5503debd9a519
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
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
 [  **@publisher**  =] **'***發行者***'**  
 這是發行者的名稱。 *發行者*是**sysname**，所有的預設值。  
  
 [  **@publisher_db**  =] **'***publisher_db***'**  
 這是發行者資料庫的名稱。 *publisher_db*是**sysname**，所有的預設值。  
  
 [  **@publication**  =] **'***發行集***'**  
 這是發行集的名稱。 *發行集*是**sysname**，所有的預設值。  
  
 [  **@upload_first**  =] **'***upload_first***'**  
 這是指在訂閱重新初始化之前，是否上傳在訂閱者端的變更。 *upload_first*是**nvarchar （5)**，預設值是 FALSE。 如果**true**，訂閱重新初始化之前上傳變更。 如果**false**，不會上傳變更。  
  
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
  
## <a name="see-also"></a>請參閱＜  
 [重新初始化訂閱](../../relational-databases/replication/reinitialize-a-subscription.md)   
 [重新初始化訂閱](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
