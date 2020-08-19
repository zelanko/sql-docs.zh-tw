---
description: sp_syscollector_set_cache_directory (Transact-SQL)
title: sp_syscollector_set_cache_directory (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_set_cache_directory_TSQL
- sp_syscollector_set_cache_directory
dev_langs:
- TSQL
helpviewer_keywords:
- data collector [SQL Server], stored procedures
- sp_syscollector_set_cache_directory stored procedure
ms.assetid: df56d5a5-8961-494f-a745-d752ca63805a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: dd4f3a049a0433ed41c9ebb1f82f6f16f6222544
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88469186"
---
# <a name="sp_syscollector_set_cache_directory-transact-sql"></a>sp_syscollector_set_cache_directory (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  指定在收集而來的資料上傳到管理資料倉儲之前，儲存這些資料的目錄。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_syscollector_set_cache_directory [ @cache_directory = ] 'cache_directory'  
```  
  
## <a name="arguments"></a>引數  
`[ @cache_directory = ] 'cache_directory'` 檔案系統中暫時儲存所收集資料的目錄。 *cache_directory* 是 **Nvarchar (255) **，預設值是 Null。 如果沒有指定任何值，則會使用預設暫存 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目錄。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 您必須先停用資料收集器，然後再變更快取目錄組態。 如果資料收集器為啟用狀態，這個預存程序就會失敗。 如需詳細資訊，請參閱 [啟用或停用資料收集](../../relational-databases/data-collection/enable-or-disable-data-collection.md)和 [管理資料收集](../../relational-databases/data-collection/manage-data-collection.md)。  
  
 執行 sp_syscollector_set_cache_directory 時，指定的目錄不需要存在;不過，在建立目錄之前，無法成功快取和上傳資料。 我們建議在執行這個預存程序之前，先建立目錄。  
  
## <a name="permissions"></a>權限  
 需要 dc_admin (具有 EXECUTE 權限) 固定資料庫角色中的成員資格，才能執行此程序。  
  
## <a name="examples"></a>範例  
 下列範例會停用資料收集器、將資料收集器的快取目錄設定為 `D:\tempdata` ，然後啟用資料收集器。  
  
```sql  
USE msdb;  
GO  
EXECUTE dbo.sp_syscollector_disable_collector;  
GO  
EXEC dbo.sp_syscollector_set_cache_directory N'D:\tempdata';  
GO  
EXECUTE dbo.sp_syscollector_enable_collector;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料收集器預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [sp_syscollector_set_cache_window &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-cache-window-transact-sql.md)  
  
  
