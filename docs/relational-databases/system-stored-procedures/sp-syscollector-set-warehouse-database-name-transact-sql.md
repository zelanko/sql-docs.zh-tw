---
title: sp_syscollector_set_warehouse_database_name （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_set_warehouse_database_name
- sp_syscollector_set_warehouse_database_name_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_set_warehouse_database_name
- data collector [SQL Server], stored procedures
ms.assetid: a85aca1b-8135-4c81-9a05-da5aec76f1ed
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 86b5037b1aa581dd99385c9be13ea58ee8a571dd
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85892855"
---
# <a name="sp_syscollector_set_warehouse_database_name-transact-sql"></a>sp_syscollector_set_warehouse_database_name (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  指定資料庫名稱 (定義於用來連接至管理資料倉儲的連接字串中)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_syscollector_set_warehouse_database_name [ @database_name = ] 'database_name'  
```  
  
## <a name="arguments"></a>引數  
 [ @database_name =] '*database_name*'  
 這是管理資料倉儲的名稱。 *database_name*是**sysname** ，預設值是 Null。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 您必須先停用資料收集器，然後再變更資料收集器範圍組態。 如果資料收集器為啟用狀態，這個程序就會失敗。  
  
 若要查看目前的資料庫名稱，請查詢[syscollector_config_store](../../relational-databases/system-catalog-views/syscollector-config-store-transact-sql.md)系統檢視。  
  
## <a name="permissions"></a>權限  
 需要 dc_admin (具有 EXECUTE 權限) 固定資料庫角色中的成員資格，才能執行此程序。  
  
## <a name="examples"></a>範例  
 下列範例會將管理資料倉儲的名稱設定為 `RemoteMDW`。  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_set_warehouse_database_name N'RemoteMDW';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
