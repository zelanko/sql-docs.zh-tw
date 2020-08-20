---
description: sp_resetstatus (Transact-SQL)
title: sp_resetstatus (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_resetstatus
- sp_resetstatus_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_resetstatus
ms.assetid: b892727f-ea3b-4b94-88d9-f2386ad4962c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7b933535fb9c1d4cf06fa52be6ccf6dbba61ff2d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88464016"
---
# <a name="sp_resetstatus-transact-sql"></a>sp_resetstatus (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  重設質疑資料庫的狀態。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 請改用 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) 。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_resetstatus [ @dbname = ] 'database'  
```  
  
## <a name="arguments"></a>引數  
 [ @dbname =] '*資料庫*'  
 這是要重設的資料庫名稱。 *資料庫* 是 **sysname**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 sp_resetstatus 會關閉資料庫的可疑旗標。 這個程序會更新 sys.databases 中具名資料庫的模式和狀態資料行。 您應該先參閱 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄並解決所有問題，再執行這個程序。 請先執行 sp_resetstatus，再停止和重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。  
  
 資料庫會因為許多原因而變成可疑。 可能的原因包括作業系統拒絕存取資料庫資源，以及一個或多個資料庫檔案無法使用或損毀。  
  
## <a name="permissions"></a>權限  
 需要系統管理員 (sysadmin) 固定伺服器角色中的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會重設 `AdventureWorks2012` 資料庫的狀態。  
  
```  
EXEC sp_resetstatus 'AdventureWorks2012';  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的系統預存程式 ](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [&#40;Transact-sql&#41;的資料庫引擎預存程式 ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)  
  
  
