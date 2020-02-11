---
title: sp_deletetracertokenhistory （Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: cf591964e5dfef0536c79b0b35e5918d4f46d972
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68771145"
---
# <a name="sp_deletetracertokenhistory-transact-sql"></a>sp_deletetracertokenhistory (Transact-SQL)

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

從[MStracer_tokens &#40;transact-sql&#41;](../../relational-databases/system-tables/mstracer-tokens-transact-sql.md)和[MStracer_history &#40;transact-sql&#41;](../../relational-databases/system-tables/mstracer-history-transact-sql.md)系統資料表中移除追蹤 token 記錄。 這個預存程序是在發行集資料庫的發行者端，或散發資料庫的散發者端執行。

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
這是追蹤 Token 插入其中之發行集的名稱。 資料類型為**sysname**。 此為必要參數。

`[ @tracer_id= ] tracer_id`  
這是要刪除之追蹤 Token 的識別碼。 資料類型為**int**。預設值為*null*。 如果是*null*，則會刪除屬於發行集的所有追蹤 token。

`[ @cutoff_date= ] cutoff_date`  
在刪除此日期之前，插入發行集的追蹤 token。 資料類型為**datetime**。 預設值為*null*。

`[ @publisher= ] 'publisher'`  
這是發行者的名稱。 資料類型為**sysname**。 預設值為*null*。

> [!NOTE]
> 只有在非[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者或從散發者執行預存程式時，才應該指定這個參數。

`[ @publisher_db= ] 'publisher_db'`  
這是發行集資料庫的名稱。 資料類型為**sysname**。 預設值是 NULL。 如果預存程序執行於發行者端，則會忽略這個參數。

> [!NOTE]
> 從散發者執行預存程式時，應該指定這個參數。

## <a name="return-code-values"></a>傳回碼值

**0** （成功）或**1** （失敗）

## <a name="remarks"></a>備註

**sp_deletetracertokenhistory**用於異動複寫中。  

如果您同時指定參數*tracer_id*和*cutoff_date*，就會發生錯誤。

如果您未執行**sp_deletetracertokenhistory**來刪除追蹤 token 中繼資料，則會在定期排程的歷程記錄清除發生時刪除資訊。

追蹤 token 識別碼可以藉由執行[sp_helptracertokens &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helptracertokens-transact-sql.md) ，或藉由查詢[MStracer_tokens &#40;transact-sql&#41;](../../relational-databases/system-tables/mstracer-tokens-transact-sql.md)系統資料表來判斷。

## <a name="permissions"></a>權限

只有下列人員才有權執行**sp_deletetracertokenhistory**：

- 散發資料庫中**replmonitor**角色的成員
- **系統管理員（sysadmin** ）固定伺服器角色的成員。
- 發行集資料庫中**db_owner**固定資料庫角色的成員。
- 固定資料庫的**db_owner** 。

## <a name="see-also"></a>另請參閱

[針對異動複寫測量延遲及驗證連接](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)

[sp_helptracertokenhistory &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md)
