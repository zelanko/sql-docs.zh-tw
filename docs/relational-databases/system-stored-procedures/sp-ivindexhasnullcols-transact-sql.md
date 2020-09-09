---
description: sp_ivindexhasnullcols (Transact-SQL)
title: sp_ivindexhasnullcols (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_ivindexhasnullcols
- sp_ivindexhasnullcols_TSQL
helpviewer_keywords:
- sp_ivindexhasnullcols
ms.assetid: ed2cde63-37e1-43cf-b6ba-3b6114a0f797
author: markingmyname
ms.author: maghan
ms.openlocfilehash: fe91514a87999bb053f6011e74b3b96ec075fbf4
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89549599"
---
# <a name="sp_ivindexhasnullcols-transact-sql"></a>sp_ivindexhasnullcols (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  驗證索引檢視的叢集索引是唯一的，且並未包含將利用索引檢視來建立交易式發行集時，可為 Null 值的任何資料行。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_ivindexhasnullcols [ @viewname = ] 'view_name'  
        , [ @fhasnullcols= ] field_has_null_columns OUTPUT  
```  
  
## <a name="arguments"></a>引數  
`[ @viewname = ] 'view_name'` 這是要驗證的視圖名稱。 *view_name* 是 **sysname**，沒有預設值。  
  
`[ @fhasnullcols = ] field_has_null_columns OUTPUT` 這是一個旗標，指出視圖索引是否有允許 Null 的資料行。 *view_name* 是 **sysname**，沒有預設值。 如果視圖索引有允許 Null 的資料行，則傳回值 **1** 。 如果視圖不包含允許 Null 的資料行，則傳回 **0** 值。  
  
> [!NOTE]  
>  如果預存程式本身傳回錯誤碼 **1**，表示預存程式執行發生失敗，則此值為 **0** ，應予以忽略。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_ivindexhasnullcols** 是由異動複寫使用。  
  
 依預設，發行集中的索引檢視發行項會建立成訂閱者端的資料表。 不過，當索引資料行允許 NULL 值時，會將索引檢視建立成在訂閱者端的索引檢視，而非資料表。 當執行這個預存程序時，它可以警示使用者目前的索引檢視有沒有這個問題。  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色或 **db_owner** 固定資料庫角色的成員，才能夠執行 **sp_ivindexhasnullcols**。  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
