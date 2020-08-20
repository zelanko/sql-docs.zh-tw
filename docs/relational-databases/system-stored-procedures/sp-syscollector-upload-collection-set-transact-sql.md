---
description: sp_syscollector_upload_collection_set (Transact-SQL)
title: sp_syscollector_upload_collection_set (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_upload_collection_set
- sp_syscollector_upload_collection_set_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_upload_collection_set
- data collector [SQL Server], stored procedures
ms.assetid: eed9232c-2b0a-4b6a-8ba0-76b7c99f48dc
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7ae866b15b11d88f7cea301e7c687edf75c9fb2f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88485641"
---
# <a name="sp_syscollector_upload_collection_set-transact-sql"></a>sp_syscollector_upload_collection_set (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  如果收集組已啟用，就會啟動收集組資料的上傳作業。  
  
> [!IMPORTANT]  
>  此程序只能用於已設定快取模式資料收集和上傳的收集組。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_syscollector_upload_collection_set [[ @collection_set_id = ] collection_set_id ]  
          , [[ @name = ] 'name' ]   
```  
  
## <a name="arguments"></a>引數  
`[ @collection_set_id = ] collection_set_id` 這是收集組的唯一本機識別碼。 *collection_set_id* 為 **int** ，而且如果 *name* 為 Null，則必須具有值。  
  
`[ @name = ] 'name'` 這是收集組的名稱。 *名稱* 是 **sysname** ，而且如果 *collection_set_id* 為 Null，則必須有值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 *Collection_set_id*或*名稱*都必須有值;兩者都不能是 Null。  
  
 這個程序可用於針對執行中的收集組啟動視需要的上傳。 它只能用於已設定快取模式資料收集和上傳的收集組。 如此可讓使用者取得要分析的資料，而不需要等候排定的上傳。  
  
## <a name="permissions"></a>權限  
 需要 **dc_operator** (中具有 execute 許可權) 固定資料庫角色的成員資格，才能執行此程式。  
  
## <a name="example"></a>範例  
 針對名為 `Simple Collection Set` 的收集組進行視需要的上傳。  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_upload_collection_set @name = 'Simple Collection Set' ;  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的系統預存程式 ](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [[資料收集]](../../relational-databases/data-collection/data-collection.md)  
  
  
