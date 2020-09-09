---
description: sp_helptracertokenhistory (Transact-SQL)
title: sp_helptracertokenhistory (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helptracertokenhistory_TSQL
- sp_helptracertokenhistory
helpviewer_keywords:
- sp_helptracertokenhistory
ms.assetid: 96910d1c-be76-43eb-9c93-4477e6761749
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4874af1c1defd949f4744a98f9f959995bf1d231
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547927"
---
# <a name="sp_helptracertokenhistory-transact-sql"></a>sp_helptracertokenhistory (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  傳回指定追蹤 Token 的詳細延遲資訊，每個訂閱者會傳回一個資料列。 這個預存程序是在發行集資料庫的發行者端，或散發資料庫的散發者端執行。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helptracertokenhistory [ @publication = ] 'publication'   
        , [ @tracer_id = ] tracer_id  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publisher_db' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'` 這是插入追蹤 token 的發行集名稱。 *發行* 集是 **sysname**，沒有預設值。  
  
`[ @tracer_id = ] tracer_id` 這是傳回的記錄資訊 [MStracer_tokens &#40;transact-sql&#41;](../../relational-databases/system-tables/mstracer-tokens-transact-sql.md) 資料表中的追蹤 token 識別碼。 *tracer_id* 是 **int**，沒有預設值。  
  
`[ @publisher = ] 'publisher'` 發行者的名稱。 *publisher* 是 **sysname**，預設值是 Null。  
  
> [!NOTE]
>  這個參數只能針對非 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者指定。  
  
`[ @publisher_db = ] 'publisher_db'` 發行集資料庫的名稱。 *publisher_db* 是 **sysname**，預設值是 Null。 如果預存程序執行於發行者端，則會忽略這個參數。  
  
## <a name="result-set"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**distributor_latency**|**bigint**|在發行者端認可的追蹤 Token 記錄和在散發者端認可的記錄之間的秒數。|  
|**使用者**|**sysname**|接收追蹤 Token 的訂閱者名稱。|  
|**subscriber_db**|**sysname**|追蹤 Token 記錄插入其中的訂閱資料庫名稱。|  
|**subscriber_latency**|**bigint**|在散發者端認可的追蹤 Token 記錄和在訂閱者端認可的記錄之間的秒數。|  
|**overall_latency**|**bigint**|在發行者端認可的追蹤 Token 記錄和在訂閱者端認可的 Token 記錄之間的秒數。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_helptracertokenhistory** 用於異動複寫中。  
  
 執行 [sp_helptracertokens &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helptracertokens-transact-sql.md) 取得發行集的追蹤 token 清單。  
  
 結果集中的 NULL 值表示無法計算延遲統計資料。 這是因為散發者端或某個訂閱者端尚未收到追蹤 Token。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_tracertokens](../../relational-databases/replication/codesnippet/tsql/sp-helptracertokenhistor_1.sql)]  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色的成員、發行集資料庫中的 **db_owner** 固定資料庫角色，或散發資料庫中的 **db_owner** 固定資料庫或 **replmonitor** 角色，才能執行 **sp_helptracertokenhistory**。  
  
## <a name="see-also"></a>另請參閱  
 [測量異動複寫的延遲並驗證連接](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)   
 [sp_deletetracertokenhistory &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-deletetracertokenhistory-transact-sql.md)  
  
  
