---
title: sp_syscollector_set_cache_window （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_set_cache_window
- sp_syscollector_set_cache_window_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_set_cache_window stored procedure
- data collector [SQL Server], stored procedures
ms.assetid: 660f2749-392f-46bf-89f3-27764d848507
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e4e37e40aea88ec90da7c95065f33f2becfe2b5f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85760023"
---
# <a name="sp_syscollector_set_cache_window-transact-sql"></a>sp_syscollector_set_cache_window (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  設定在發生失敗的情況下嘗試進行資料上傳的次數。 在失敗時重試上傳可減少遺失所收集資料的風險。  

  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_syscollector_set_cache_window [ @cache_window = ] cache_window   
```  
  
## <a name="arguments"></a>引數  
 [ @cache_window =] *cache_window*  
 這是在不遺失資料的情況下，重試將資料上傳至管理資料倉儲，但卻失敗的次數。 *cache_window*是**int** ，預設值是1。 *cache_window*可以具有下列其中一個值：  
  
|值|說明|  
|-----------|-----------------|  
|-1|從先前上傳失敗中快取所有上傳資料。|  
|0|不要從上傳失敗中快取任何資料。|  
|*n*|從 n 個先前的上傳失敗中快取資料，其中*n* >= 1。|  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 您必須先停用資料收集器，然後再變更快取視窗組態。 如果資料收集器為啟用狀態，這個預存程序就會失敗。 如需詳細資訊，請參閱[啟用或停用資料收集](../../relational-databases/data-collection/enable-or-disable-data-collection.md)和[管理資料收集](../../relational-databases/data-collection/manage-data-collection.md)。  
  
## <a name="permissions"></a>權限  
 需要 dc_admin (具有 EXECUTE 權限) 固定資料庫角色中的成員資格，才能執行此程序。  
  
## <a name="examples"></a>範例  
 下列範例會停用資料收集器、將快取視窗設定為保留最多三次上傳失敗的資料，然後再啟用資料收集器。  
  
```sql  
USE msdb;  
GO  
EXECUTE dbo.sp_syscollector_disable_collector;  
GO  
EXECUTE dbo.sp_syscollector_set_cache_window 3;  
GO  
EXECUTE dbo.sp_syscollector_enable_collector;  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的系統預存程式](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_syscollector_set_cache_directory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-cache-directory-transact-sql.md)  
  
  
