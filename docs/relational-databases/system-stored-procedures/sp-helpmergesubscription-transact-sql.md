---
title: sp_helpmergesubscription (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergesubscription
- sp_helpmergesubscription_TSQL
helpviewer_keywords:
- sp_helpmergesubscription
ms.assetid: da564112-f769-4e67-9251-5699823e8c86
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4643cfc08db68e5369cfca25d2de76d314ffb347
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58530670"
---
# <a name="sphelpmergesubscription-transact-sql"></a>sp_helpmergesubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  將訂閱的相關資訊傳回合併式發行集，發送和提取訂閱都包括在內。 這個預存程序執行於發行集資料庫的發行者端，或訂閱資料庫的重新發行訂閱者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helpmergesubscription [ [ @publication=] 'publication']  
    [ , [ @subscriber=] 'subscriber']  
    [ , [ @subscriber_db=] 'subscriber_db']  
    [ , [ @publisher=] 'publisher']  
    [ , [ @publisher_db=] 'publisher_db']  
    [ , [ @subscription_type=] 'subscription_type']  
    [ , [ @found=] 'found' OUTPUT]  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'` 是發行集名稱。 *發行集*已**sysname**，預設值是**%**。 發行集必須已存在，且符合識別碼的規則。 如果是 NULL 或**%**，會傳回所有合併式發行集和目前的資料庫中的訂用帳戶的相關資訊。  
  
`[ @subscriber = ] 'subscriber'` 是訂閱者的名稱。 *訂閱者*已**sysname**，預設值是**%**。 如果是 NULL 或 %，就會傳回給定發行集之所有訂閱的相關資訊。  
  
`[ @subscriber_db = ] 'subscriber_db'` 是訂閱資料庫的名稱。 *subscriber_db*已**sysname**，預設值是**%**，傳回所有訂閱資料庫的相關資訊。  
  
`[ @publisher = ] 'publisher'` 是 「 發行者 」 的名稱。 發行者必須是有效伺服器。 *發行者*已**sysname**，預設值是**%**，它會傳回所有發行者的相關資訊。  
  
`[ @publisher_db = ] 'publisher_db'` 是發行者資料庫的名稱。 *publisher_db*已**sysname**，預設值是**%**，傳回所有發行者資料庫的相關資訊。  
  
`[ @subscription_type = ] 'subscription_type'` 是訂用帳戶的類型。 *subscription_type*已**nvarchar(15)**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**推播**（預設值）|發送訂閱|  
|**pull**|提取訂閱|  
|**兩者**|發送訂閱和提取訂閱|  
  
`[ @found = ] 'found'OUTPUT` 是指示傳回資料列的旗標。 *找到*已**int**和一個 OUTPUT 參數，預設值是 NULL。 **1**表示找到發行集。 **0**指出找不到發行集。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**subscription_name**|**sysname**|訂閱的名稱。|  
|**publication**|**sysname**|發行集的名稱。|  
|**發行者**|**sysname**|發行者的名稱。|  
|**publisher_db**|**sysname**|發行者資料庫的名稱。|  
|**訂閱者**|**sysname**|訂閱者的名稱。|  
|**subscriber_db**|**sysname**|訂閱資料庫的名稱。|  
|**status**|**int**|訂閱的狀態：<br /><br /> **0** = 所有作業都在等待啟動<br /><br /> **1** = 一或多項作業會啟動<br /><br /> **2** = 所有作業都已執行成功<br /><br /> **3** = 至少一個作業正在執行<br /><br /> **4** = 所有作業都已排程且閒置<br /><br /> **5** = 至少一項作業嘗試在上一次失敗之後執行<br /><br /> **6** = 至少一項工作已順利執行失敗|  
|**subscriber_type**|**int**|訂閱者的類型。|  
|**subscription_type**|**int**|訂閱的類型：<br /><br /> **0** = 發送<br /><br /> **1** = 提取<br /><br /> **2** = 兩者|  
|**priority**|**float(8)**|表示訂閱優先權的數字。|  
|**sync_type**|**tinyint**|訂閱同步處理類型。|  
|**description**|**nvarchar(255)**|這項合併訂閱的簡要描述。|  
|**merge_jobid**|**binary(16)**|合併代理程式的作業識別碼。|  
|**full_publication**|**tinyint**|這是指訂閱完整或篩選發行集。|  
|**offload_enabled**|**bit**|指定是否已將複寫代理程式的卸載執行設成執行於訂閱者端。 如果是 NULL，就是執行於發行者端。|  
|**offload_server**|**sysname**|執行代理程式的伺服器名稱。|  
|**use_interactive_resolver**|**int**|傳回是否在重新調整期間使用互動式解析程式。 如果**0**，不會使用互動式解析程式。|  
|**hostname**|**sysname**|值來篩選訂閱時所提供的值[HOST_NAME](../../t-sql/functions/host-name-transact-sql.md)函式。|  
|**subscriber_security_mode**|**smallint**|這是安全性模式，在訂閱者，其中**1**表示 Windows 驗證，並**0**表示[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證。|  
|**subscriber_login**|**sysname**|這是在訂閱者端的登入名稱。|  
|**subscriber_password**|**sysname**|永遠不傳回實際的訂閱者密碼。 結果會藉由遮罩 」**\*\*\*\*\*\***"字串。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_helpmergesubscription**合併式複寫中用來傳回儲存在 「 發行者 」 或重新發行訂閱者的訂用帳戶資訊。  
  
 匿名訂閱，如*subscription_type*值一律是**1** （提取）。 不過，您必須執行[sp_helpmergepullsubscription](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md)匿名訂閱的資訊到訂閱者端。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定伺服器角色**db_owner**固定的資料庫角色或訂閱所屬發行集之發行集存取清單能夠執行**sp_helpmergesubscription**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_addmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)   
 [sp_changemergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md)   
 [sp_dropmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
