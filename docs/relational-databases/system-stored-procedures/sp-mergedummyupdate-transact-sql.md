---
description: sp_mergedummyupdate (Transact-SQL)
title: sp_mergedummyupdate (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_mergedummyupdate_TSQL
- sp_mergedummyupdate
helpviewer_keywords:
- sp_mergedummyupdate
ms.assetid: b834f7f6-9588-4d59-a3e2-83d8e8e722e1
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: dbacf385842d226c733c5c1baec9859f26e140d3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88464128"
---
# <a name="sp_mergedummyupdate-transact-sql"></a>sp_mergedummyupdate (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  執行給定資料列的虛擬更新，以便在下次合併期間重新傳送它。 這個預存程序可執行於發行集資料庫的發行者端，或訂閱資料庫的訂閱者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_mergedummyupdate [ @source_object =] 'source_object', [ @rowguid =] 'rowguid'  
```  
  
## <a name="arguments"></a>引數  
`[ @source_object = ] 'source_object'` 這是來源物件的名稱。 *source_object*是 **Nvarchar (386) **，沒有預設值。  
  
`[ @rowguid = ] 'rowguid'` 這是資料列識別碼。 *rowguid* 是 **uniqueidentifier**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_mergedummyupdate** 用於合併式複寫中。  
  
 如果您自行撰寫複寫衝突檢視器 ( # A0) 的替代方案， **sp_mergedummyupdate**會很有用。  
  
## <a name="permissions"></a>權限  
 只有 **db_owner** 固定資料庫角色的成員，才能夠執行 **sp_mergedummyupdate**。  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
