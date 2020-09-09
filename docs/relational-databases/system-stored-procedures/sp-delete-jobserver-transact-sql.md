---
description: sp_delete_jobserver (Transact-SQL)
title: sp_delete_jobserver (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_jobserver
- sp_delete_jobserver_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_jobserver
ms.assetid: 6d63ed32-68cf-4d8f-aa40-05a3826e05b8
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4db36a6fbcf09ca6758fd3838ab489bc6aa23cb2
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546139"
---
# <a name="sp_delete_jobserver-transact-sql"></a>sp_delete_jobserver (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  移除指定的目標伺服器。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_delete_jobserver { [ @job_id = ] job_id | [ @job_name = ] 'job_name' } ,   
     [ @server_name = ] 'server'  
```  
  
## <a name="arguments"></a>引數  
`[ @job_id = ] job_id` 將從中移除指定目標伺服器之作業的識別碼。 *job_id* 是 **uniqueidentifier**，預設值是 Null。  
  
`[ @job_name = ] 'job_name'` 將從中移除指定目標伺服器之作業的名稱。 *job_name* 是 **sysname**，預設值是 Null。  
  
> [!NOTE]  
>  必須指定 *job_id* 或 *job_name* ;不可同時指定兩者。  
  
`[ @server_name = ] 'server'` 要從指定作業中移除的目標伺服器名稱。 *伺服器* 是 **Nvarchar (30) **，沒有預設值。 *伺服器* 可以 ** (本機) **或遠端目標伺服器的名稱。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="permissions"></a>權限  
 若要執行這個預存程式，使用者必須是 **系統管理員（sysadmin** ）固定伺服器角色的成員。  
  
## <a name="examples"></a>範例  
 下列範例會 `SEATTLE2` 從處理作業中移除伺服器 `Weekly Sales Backups` 。  
  
> [!NOTE]  
>  這個範例假設先前已建立 `Weekly Sales Backups` 作業。  
  
```  
USE msdb ;  
GO  
  
EXEC sp_delete_jobserver  
    @job_name = N'Weekly Sales Backups',  
    @server_name = N'SEATTLE2' ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_add_jobserver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)   
 [sp_help_jobserver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-jobserver-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
