---
description: sp_getqueuedrows (Transact-SQL)
title: sp_getqueuedrows (Transact-sql) |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 6948964a224d0dfe1d36324971608e649ec45d4e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88481249"
---
# <a name="sp_getqueuedrows-transact-sql"></a>sp_getqueuedrows (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  擷取訂閱者有更新在佇列中暫止的資料列。 這個預存程序執行於訂閱資料庫的訂閱者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_getqueuedrows [ @tablename = ] 'tablename'  
    [ , [ @owner = ] 'owner'  
    [ , [ @tranid = ] 'transaction_id' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @tablename = ] 'tablename'` 這是資料表的名稱。 *tablename* 是 **sysname**，沒有預設值。 這份資料表必須在佇列訂閱中。  
  
`[ @owner = ] 'owner'` 這是訂用帳戶擁有者。 *owner* 是 **sysname**，預設值是 Null。  
  
`[ @tranid = ] 'transaction_id'` 允許依交易識別碼來篩選輸出。 *transaction_id* 是 **Nvarchar (70) **，預設值是 Null。 如果指定的話，便會顯示佇列命令的相關聯交易識別碼。 如果是 NULL，便會顯示佇列中的所有命令。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="result-sets"></a>結果集  
 顯示目前至少有訂閱資料表的一項佇列交易的所有資料列。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**動作**|**Nvarchar (10) **|進行同步處理時所採取的動作類型。<br /><br /> INS= 插入<br /><br /> DEL = 刪除<br /><br /> UPD = 更新|  
|**Tranid**|**Nvarchar (70) **|用來執行命令的交易識別碼。|  
|**table column1...n**||資料表 *表中指定*之資料表的每個資料行的值。|  
|**msrepl_tran_version**|**uniqueidentifier**|這個資料行用來追蹤複寫資料的變更，以及在發行者端執行衝突偵測。 這個資料行會自動加入資料表中。|  
  
## <a name="remarks"></a>備註  
 **sp_getqueuedrows** 是在參與佇列更新的訂閱者端使用。  
  
 **sp_getqueuedrows** 在已參與佇列更新的訂閱資料庫上尋找給定資料表的資料列，但目前尚未由佇列讀取器代理程式解決。  
  
## <a name="permissions"></a>權限  
 **sp_getqueuedrows** 需要 *tablename*中指定之資料表的 SELECT 許可權。  
  
## <a name="see-also"></a>另請參閱  
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [佇列更新衝突偵測和解決方式](../../relational-databases/replication/transactional/updatable-subscriptions-queued-updating-conflict-resolution.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
