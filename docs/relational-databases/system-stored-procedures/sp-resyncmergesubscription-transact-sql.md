---
title: sp_resyncmergesubscription (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/04/2017
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
- sp_resyncmergesubscription_TSQL
- sp_resyncmergesubscription
helpviewer_keywords:
- sp_resyncmergesubscription
ms.assetid: e04d464a-60ab-4b39-a710-c066025708e6
caps.latest.revision: 19
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 35f5311da7b2d878a738695ee62a65c947f98693
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="spresyncmergesubscription-transact-sql"></a>sp_resyncmergesubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  將合併訂閱重新同步處理到您指定的已知驗證狀態。 這可讓您將訂閱資料庫強制聚合或同步處理到某個特定的時間點，如上次驗證成功或指定的日期。 當利用這個方法來重新同步處理訂閱時，不會重新套用快照集。 快照式複寫訂閱或異動複寫訂閱不使用這個預存程序。 這個預存程序執行於發行集資料庫的發行者端，或訂閱資料庫的訂閱者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_resyncmergesubscription [ [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publisher_db' ]  
        , [ @publication = ] 'publication'   
    [ , [ @subscriber = ] 'subscriber' ]  
    [ , [ @subscriber_db = ] 'subscriber_db' ]  
    [ , [ @resync_type = ] resync_type ]  
    [ , [ @resync_date_str = ] resync_date_string ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@publisher** = ] **'***publisher***'**  
 這是發行者的名稱。 *發行者*是**sysname**，預設值是 NULL。 如果預存程序執行於發行者端，NULL 值就有效。 如果預存程序執行於訂閱者端，就必須指定發行者。  
  
 [ **@publisher_db** = ] **'***publisher_db***'**  
 這是發行集資料庫的名稱。 *publisher_db*是**sysname**，預設值是 NULL。 如果預存程序執行於發行集資料庫中的發行者端，NULL 值就有效。 如果預存程序執行於訂閱者端，就必須指定發行者。  
  
 [ **@publication** = ] **'***publication***'**  
 這是發行集的名稱。 *發行集*是**sysname**，沒有預設值。  
  
 [ **@subscriber** = ] **'***subscriber***'**  
 這是訂閱者的名稱。 *訂閱者*是**sysname**，預設值是 NULL。 如果預存程序執行於訂閱者端，NULL 值就有效。 如果預存程序執行於發行者端，就必須指定訂閱者。  
  
 [ **@subscriber_db** = ] **'***subscriber_db***'**  
 這是訂閱資料庫的名稱。 *subscription_db*是**sysname**，預設值是 NULL。 如果預存程序執行於訂閱資料庫中的訂閱者端，NULL 值就有效。 如果預存程序執行於發行者端，就必須指定訂閱者。  
  
 [ **@resync_type** = ] *resync_type*  
 定義應該開始重新同步的時間。 *resync_type*是**int**，而且可以是下列值之一。  
  
|Value|描述|  
|-----------|-----------------|  
|**0**|從初始快照集之後開始同步處理。 這是最需要資源的選項，因為訂閱者會套用初始快照集之後的所有變更。|  
|**1**|從上次驗證成功之後開始同步處理。 訂閱者會重新套用上次驗證成功之後所引發的所有新的或不完整的層代 (Generation)。|  
|**2**|從所提供的日期開始同步處理*resync_date_str*。 訂閱者會重新套用這個日期之後所引發的所有新的或不完整的層代 (Generation)。|  
  
 [ **@resync_date_str=**] *resync_date_string*  
 定義應該開始重新同步的日期。 *resync_date_string*是**nvarchar （30)**，預設值是 NULL。 使用這個參數時*resync_type*值**2**。 指定的資料會轉換成其對等**datetime**值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_resyncmergesubscription**用於合併式複寫中。  
  
 值為**0**如*resync_type*參數，其會在初始快照集之後，重新套用所有變更，可能是耗費資源，但可能不會比完整重新初始化。 例如，如果初始快照集是一個月前所傳遞的，這個值會造成重新套用上個月以來的資料。 如果初始快照集包含 1 GB 資料，但上個月以來的變更量含有 2 MB 已變更的資料，重新套用這些資料的效率，可能比重新套用完整的 1 GB 快照集好。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_resyncmergesubscription**。  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
