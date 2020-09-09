---
description: sp_helptracertokens (Transact-SQL)
title: sp_helptracertokens (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helptracertokens
- sp_helptracertokens_TSQL
helpviewer_keywords:
- sp_helptracertokens
ms.assetid: 61f27234-531d-4b37-8fa3-fe4c32e6f521
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 190e1471760fdda69acfa18075ac14833b57cc42
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547920"
---
# <a name="sp_helptracertokens-transact-sql"></a>sp_helptracertokens (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  針對插入發行集以判斷延遲的每個追蹤 Token，各傳回一個資料列。 這個預存程序是在發行集資料庫的發行者端，或散發資料庫的散發者端執行。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helptracertokens [ @publication = ] 'publication'   
    [ , [ @publisher = ] 'publisher' ]   
    [ , [ @publisher_db = ] 'publisher_db' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'` 這是插入追蹤 token 的發行集名稱。 *發行* 集是 **sysname**，沒有預設值。  
  
`[ @publisher = ] 'publisher'` 發行者的名稱。 *publisher* 是 **sysname**，預設值是 Null。  
  
> [!NOTE]
>  這個參數只能針對非 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者指定。  
  
`[ @publisher_db = ] 'publisher_db'` 發行集資料庫的名稱。 *publisher_db* 是 **sysname**，預設值是 Null。 如果預存程序執行於發行者端，則會忽略這個參數。  
  
## <a name="result-set"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**tracer_id**|**int**|識別追蹤 Token 記錄。|  
|**publisher_commit**|**datetime**|在發行集資料庫的發行者端認可 Token 記錄的日期和時間。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_helptracertokens** 用於異動複寫中。  
  
 **sp_helptracertokens** 用來在執行 [sp_helptracertokenhistory &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md)時取得追蹤 token 識別碼。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_tracertokens](../../relational-databases/replication/codesnippet/tsql/sp-helptracertokens-tran_1.sql)]  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色的成員、發行集資料庫中的 **db_owner** 固定資料庫角色，或散發資料庫中的 **db_owner** 固定資料庫或 **replmonitor** 角色，才能執行 **sp_helptracertokenhistory**。  
  
## <a name="see-also"></a>另請參閱  
 [測量異動複寫的延遲並驗證連接](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)   
 [sp_deletetracertokenhistory &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-deletetracertokenhistory-transact-sql.md)  
  
  
