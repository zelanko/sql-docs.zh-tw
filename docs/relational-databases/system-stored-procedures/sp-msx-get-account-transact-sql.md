---
title: sp_msx_get_account （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_msx_get_account_TSQL
- sp_msx_get_account
dev_langs:
- TSQL
helpviewer_keywords:
- sp_msx_get_account
ms.assetid: 7b478049-e2d0-4bac-865a-b97fd1d8dfbc
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ddb3d983b37bdad5db334073fe168b518aaee77a
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85893466"
---
# <a name="sp_msx_get_account-transact-sql"></a>sp_msx_get_account (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  列出目標伺服器用來登入主要伺服器之認證的相關資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_msx_get_account  
```  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 傳回下列結果集：  
  
|資料行名稱|類型|說明|  
|-----------------|----------|-----------------|  
|msx_connection|**int**|主要伺服器連接編號。|  
|msx_credential_id|**int**|這個主要伺服器連接所用的認證識別碼。|  
|msx_credential_name|**sysname**|這個主要伺服器連接所用的認證名稱。|  
|msx_login_name|**nvarchar(4000)**|Windows 使用者的認證網域名稱和使用者名稱。|  
  
## <a name="remarks"></a>備註  
 如果未指定這部目標伺服器的認證，會傳回空的結果集。 若要設定認證，請使用 sp_msx_set_account。  
  
## <a name="permissions"></a>權限  
 需要系統管理員 (sysadmin) 固定伺服器角色中的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會列出這部目標伺服器用來登入主要伺服器的認證資訊。  
  
```  
USE msdb ;  
GO  
  
EXECUTE dbo.sp_msx_get_account ;  
GO  
```  
  
 範例結果集如下：  
  
 `msx_connection msx_credential_id msx_credential_name  msx_login_name`  
  
 `-------------- ----------------- -------------------- ------------------------------`  
  
 `1              65538             MsxAccount           AdventureWorks2012\MsxAccount`  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Agent 預存程式 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [&#40;Transact-sql&#41;建立認證](../../t-sql/statements/create-credential-transact-sql.md)   
 [sp_msx_set_account &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-msx-set-account-transact-sql.md)  
  
  
