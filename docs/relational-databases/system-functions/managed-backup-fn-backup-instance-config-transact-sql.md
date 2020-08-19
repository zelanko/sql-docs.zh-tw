---
description: 'managed_backup fn_backup_instance_config (Transact-sql) '
title: managed_backup fn_backup_instance_config (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_backup_instance_config
- smart_admin.fn_backup_instance_config_TSQL
- fn_backup_instance_config_TSQL
- smart_admin.fn_backup_instance_config
dev_langs:
- TSQL
helpviewer_keywords:
- smart_admin.fn_backup_instance_config
- fn_backup_instance_config
ms.assetid: 2382a547-c0c9-4e1d-87c9-d8526192eb5a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a65649b7b565475eebd69bcadf4ac28bef707d7b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88419562"
---
# <a name="managed_backupfn_backup_instance_config-transact-sql"></a>managed_backup fn_backup_instance_config (Transact-sql) 
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  使用 SQL Server 執行個體的 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 預設組態設定時傳回 1 個資料列。  
  
 使用此預存程序可檢閱或判斷 SQL Server 執行個體目前的[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]預設組態設定。  
  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```sql  
managed_backup.fn_backup_db_config ()  
```  
  
##  <a name="arguments"></a><a name="Arguments"></a> 引數  
 None  
  
## <a name="table-returned"></a>傳回的資料表  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|is_smart_backup_enabled|INT|啟用[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]時顯示 1，停用[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]時顯示 0。|  
|credential_name|SYSNAME|預設 SQL 認證，用來驗證儲存體。|  
|retention_days|INT|於執行個體層級設定的預設保留週期。|  
|storage_url|NVARCHAR (1024) |於執行個體層級設定的預設儲存體帳戶 URL。|  
|encryption_algorithm|SYSNAME|加密演算法的名稱。 如果未指定加密則設為 NULL。|  
|encryptor_type|NVARCHAR (32) |使用的加密程式類型：憑證或非對稱金鑰。 如果未指定加密程式則設為 NULL。|  
|encryptor_name|SYSNAME|憑證或非對稱金鑰的名稱。 如果未指定名稱則設為 NULL|  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>權限  
 需要具有**ALTER ANY CREDENTIAL**許可權的**db_backupoperator**資料庫角色中的成員資格。 使用者不應被拒絕 **VIEW ANY DEFINITION** 許可權。  
  
## <a name="examples"></a>範例  
 下列範例會傳回執行所在之執行個體的[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]預設組態設定：  
  
```  
Use msdb;  
GO  
SELECT * FROM managed_backup.fn_backup_instance_config ();  
  
```  
  
  
