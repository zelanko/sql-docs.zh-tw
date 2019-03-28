---
title: sp_getqueuedrows (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_getqueuedrows_TSQL
- sp_getqueuedrows
helpviewer_keywords:
- sp_getqueuedrows
ms.assetid: 139e834f-1988-4b4d-ac81-db1f89ea90e8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fa6ce6b4e0d1c3fbefe7256f3ca96c84d59e664d
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58535410"
---
# <a name="spgetqueuedrows-transact-sql"></a>sp_getqueuedrows (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  擷取訂閱者有更新在佇列中暫止的資料列。 這個預存程序執行於訂閱資料庫的訂閱者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_getqueuedrows [ @tablename = ] 'tablename'  
    [ , [ @owner = ] 'owner'  
    [ , [ @tranid = ] 'transaction_id' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @tablename = ] 'tablename'` 為資料表的名稱。 *tablename*已**sysname**，沒有預設值。 這份資料表必須在佇列訂閱中。  
  
`[ @owner = ] 'owner'` 是訂用帳戶擁有者。 *擁有者*已**sysname**，預設值是 NULL。  
  
`[ @tranid = ] 'transaction_id'` 可讓交易識別碼。 所要篩選輸出 *transaction_id*已**nvarchar(70)**，預設值是 NULL。 如果指定的話，便會顯示佇列命令的相關聯交易識別碼。 如果是 NULL，便會顯示佇列中的所有命令。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 顯示目前至少有訂閱資料表的一項佇列交易的所有資料列。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**動作**|**nvarchar(10)**|進行同步處理時所採取的動作類型。<br /><br /> INS= 插入<br /><br /> DEL = 刪除<br /><br /> UPD = 更新|  
|**tranid**|**nvarchar(70)**|用來執行命令的交易識別碼。|  
|**table column1...n**||指定的資料表中的每個資料行的值*tablename*。|  
|**msrepl_tran_version**|**uniqueidentifier**|這個資料行用來追蹤複寫資料的變更，以及在發行者端執行衝突偵測。 這個資料行會自動加入資料表中。|  
  
## <a name="remarks"></a>備註  
 **sp_getqueuedrows**在參與佇列更新訂閱者使用。  
  
 **sp_getqueuedrows**訂用帳戶的指定資料表的資料列資料庫，尋找參與佇列更新，但目前尚未解決佇列讀取器代理程式。  
  
## <a name="permissions"></a>Permissions  
 **sp_getqueuedrows**要求中指定之資料表的 SELECT 權限*tablename*。  
  
## <a name="see-also"></a>另請參閱  
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [佇列更新衝突偵測和解決方法](../../relational-databases/replication/transactional/updatable-subscriptions-queued-updating-conflict-resolution.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
