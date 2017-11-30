---
title: "sp_syscollector_set_cache_directory (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_syscollector_set_cache_directory_TSQL
- sp_syscollector_set_cache_directory
dev_langs: TSQL
helpviewer_keywords:
- data collector [SQL Server], stored procedures
- sp_syscollector_set_cache_directory stored procedure
ms.assetid: df56d5a5-8961-494f-a745-d752ca63805a
caps.latest.revision: "18"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c21066f81db2e229ac66ea350a9c369174eaa4fb
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
---
# <a name="spsyscollectorsetcachedirectory-transact-sql"></a>sp_syscollector_set_cache_directory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  指定在收集而來的資料上傳到管理資料倉儲之前，儲存這些資料的目錄。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_syscollector_set_cache_directory [ @cache_directory = ] 'cache_directory'  
```  
  
## <a name="arguments"></a>引數  
 [  **@cache_directory =** ] **'***cache_directory***'**  
 檔案系統中暫時儲存所收集之資料的目錄。 *cache_directory*是**nvarchar （255)**，預設值是 NULL。 如果沒有指定任何值，則會使用預設暫存 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目錄。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 您必須先停用資料收集器，然後再變更快取目錄組態。 如果資料收集器為啟用狀態，這個預存程序就會失敗。 如需詳細資訊，請參閱[啟用或停用資料收集](../../relational-databases/data-collection/enable-or-disable-data-collection.md)，和[管理資料收集](../../relational-databases/data-collection/manage-data-collection.md)。  
  
 在執行 sp_syscollector_set_cache_directory 時候不需要有指定的目錄；不過，必須先建立目錄，才能成功地快取和上傳資料。 我們建議在執行這個預存程序之前，先建立目錄。  
  
## <a name="permissions"></a>Permissions  
 需要 dc_admin (具有 EXECUTE 權限) 固定資料庫角色中的成員資格，才能執行此程序。  
  
## <a name="examples"></a>範例  
 下列範例會停用資料收集器、 快取目錄設定資料收集器`D:\tempdata`，然後再啟用資料收集器。  
  
```tsql  
USE msdb;  
GO  
EXECUTE dbo.sp_syscollector_disable_collector;  
GO  
EXEC dbo.sp_syscollector_set_cache_directory N'D:\tempdata';  
GO  
EXECUTE dbo.sp_syscollector_enable_collector;  
GO  
```  
  
## <a name="see-also"></a>請參閱  
 [資料收集器預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [sp_syscollector_set_cache_window &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-cache-window-transact-sql.md)  
  
  
