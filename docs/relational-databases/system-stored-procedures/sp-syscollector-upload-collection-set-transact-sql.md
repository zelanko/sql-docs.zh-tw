---
title: sp_syscollector_upload_collection_set (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 19
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a872e5aaef1d59ffa0d9e73d1a175d2a6fe8b543
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="spsyscollectoruploadcollectionset-transact-sql"></a>sp_syscollector_upload_collection_set (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 [ **@collection_set_id =** ] *collection_set_id*  
 這是收集組的唯一本機識別碼。 *collection_set_id*是**int**而且必須具有值，如果*名稱*是 NULL。  
  
 [ **@name =** ] **'***name***'**  
 這是收集組的名稱。 *名稱*是**sysname**而且必須具有值，如果*collection_set_id*是 NULL。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 任一*collection_set_id*或*名稱*必須具有值，不能同時為 NULL。  
  
 這個程序可用於針對執行中的收集組啟動視需要的上傳。 它只能用於已設定快取模式資料收集和上傳的收集組。 如此可讓使用者取得要分析的資料，而不需要等候排定的上傳。  
  
## <a name="permissions"></a>Permissions  
 需要的成員資格**dc_operator** （具有 EXECUTE 權限） 固定的資料庫角色，才能執行此程序。  
  
## <a name="example"></a>範例  
 針對名為 `Simple Collection Set` 的收集組進行視需要的上傳。  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_upload_collection_set @name = 'Simple Collection Set' ;  
```  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [資料收集](../../relational-databases/data-collection/data-collection.md)  
  
  
