---
title: sp_deletetracertokenhistory & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_deletetracertokenhistory
- sp_deletetracertokenhistory_TSQL
helpviewer_keywords:
- sp_deletetracertokenhistory
ms.assetid: 9ae1be14-0d2f-40b1-9d6e-22d79726abf4
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0a7f70f5cd56867add98150d471d61cbc70faad0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68111926"
---
# <a name="spdeletetracertokenhistory-transact-sql"></a>sp_deletetracertokenhistory (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

移除追蹤 token 記錄，從[MStracer_tokens &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-tables/mstracer-tokens-transact-sql.md)並[MStracer_history &#40;-&#41; ](../../relational-databases/system-tables/mstracer-history-transact-sql.md)系統資料表。 這個預存程序是在發行集資料庫的發行者端，或散發資料庫的散發者端執行。

![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>語法

```
sp_deletetracertokenhistory [ @publication = ] 'publication'
    [ , [ @tracer_id = ] tracer_id ]
    [ , [ @cutoff_date = ] cutoff_date ]
    [ , [ @publisher = ] 'publisher' ]
    [ , [ @publisher_db = ] 'publisher_db' ]
```

## <a name="arguments"></a>引數

`@publication= 'publication'`  
這是追蹤 Token 插入其中之發行集的名稱。 資料類型是**sysname**。 此參數為必要。

`[ @tracer_id= ] tracer_id`  
這是要刪除之追蹤 Token 的識別碼。 資料類型是**int**。預設值是 *null*。 如果*null*，會刪除屬於發行集的所有追蹤 token。

`[ @cutoff_date= ] cutoff_date`  
刪除此日期之前插入發行集的追蹤 token。 資料類型是**datetime**。 預設值是 *null*。

`[ @publisher= ] 'publisher'`  
這是發行者的名稱。 資料類型是**sysname**。 預設值是 *null*。

> [!NOTE]
> 此參數應只指定非[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者或散發者 」 從執行預存程序時。

`[ @publisher_db= ] 'publisher_db'`  
這是發行集資料庫的名稱。 資料類型是**sysname**。 預設值是 NULL。 如果預存程序執行於發行者端，則會忽略這個參數。

> [!NOTE]
> 從散發者執行預存程序時，應該指定這個參數。

## <a name="return-code-values"></a>傳回碼值

**0** （成功） 或**1** （失敗）

## <a name="remarks"></a>備註

**sp_deletetracertokenhistory**用於異動複寫中。  

如果您指定兩個參數，就會發生錯誤*tracer_id*並*cutoff_date*。

如果您不會執行**sp_deletetracertokenhistory**刪除追蹤 token 中繼資料，資訊會被刪除時定期排程的記錄清除工作。

您可以藉由執行判斷追蹤 token 識別碼[sp_helptracertokens &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-helptracertokens-transact-sql.md)或藉由查詢[MStracer_tokens &#40;-&#41; ](../../relational-databases/system-tables/mstracer-tokens-transact-sql.md)系統資料表。

## <a name="permissions"></a>Permissions

只有下列人員有權限執行**sp_deletetracertokenhistory**:

- 成員**replmonitor**散發資料庫中的角色
- 成員**sysadmin**固定的伺服器角色。
- 成員**db_owner**固定的資料庫角色，發行集資料庫中。
- **Db_owner**的固定的資料庫。

## <a name="see-also"></a>另請參閱

[針對異動複寫測量延遲及驗證連接](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)

[sp_helptracertokenhistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md)
