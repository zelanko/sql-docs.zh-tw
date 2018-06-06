---
title: managed_backup.sp_set_parameter (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_set_parameter_TSQL
- sp_set_parameter
- smart_admin.sp_set_parameter
- smart_admin.sp_set_parameter_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_set_parameter
- smart_admin.sp_set_parameter
ms.assetid: bd8ae5fd-1337-4b7f-b0a4-153cbca9fa5f
caps.latest.revision: 15
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2a9f1d5eeec1fc5b24fbc1974d27e9f4b5efd00d
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="managedbackupspsetparameter-transact-sql"></a>managed_backup.sp_set_parameter (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  設定指定的 Smart Admin 系統參數值。  
  
 可用的參數與[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]相關。 這些參數可用來設定電子郵件通知、啟用特定擴充事件，以及啟用使用者設定原則式管理原則。 您必須指定參數名稱與參數值組。  

  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```sql  
EXEC managed_backup.sp_set_parameter   
    [@parameter_name = ] {'SSMBackup2WANotificationEmailIds' | 'SSMBackup2WAEnableUserDefinedPolicy' | 'SSMBackup2WADebugXevent' | 'FileRetentionDebugXevent' | 'StorageOperationDebugXevent'}  
    ,[@parameter_value = ] 'parameter_value'  
```  
  
##  <a name="Arguments"></a> 引數  
 @parameter_name  
 您要設定值之參數的名稱。 @parameter_name 是 nvarchar （128）。 可用的參數名稱是**SSMBackup2WANotificationEmailIds**， **SSMBackup2WADebugXevent**， **SSMBackup2WAEnableUserDefinedPolicy**， **FileRetentionDebugXevent**，和**StorageOperationDebugXevent**。  
  
 @parameter_value  
 您要設定之參數的值。 @parameter 值為 nvarchar （128）。  以下是允許的參數名稱與值組：  
  
-   @parameter_name = 'SSMBackup2WANotificationEmailIds': @parameter_value = 'email'  
  
-   @parameter_name = 'SSMBackup2WAEnableUserDefinedPolicy': @parameter_value = {'true' |false'}  
  
-   @parameter_name = 'SSMBackup2WADebugXevent': @parameter_value = {'true' |false'}  
  
-   @parameter_name = 'FileRetentionDebugXevent': @parameter_value = {'true' |false'}  
  
-   @parameter_name = 'StorageOperationDebugXevent' = {'true' |false'}  
  
## <a name="return-code-value"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="best-practices"></a>最佳作法  
 描述使用者執行陳述式或常式時應了解之最佳作法的選用章節。  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>Permissions  
 需要**EXECUTE**權限**managed_backup.sp_set_parameter**預存程序。  
  
## <a name="examples"></a>範例  
 下列範例啟用作業和偵錯擴充事件。  
  
```  
-- to enable operational events  
Use msdb;  
Go  
         EXEC managed_backup.sp_set_parameter 'FileRetentionOperationalXevent', 'True'  
--  to enable debug events  
Use msdb;  
Go  
         EXEC managed_backup.sp_set_parameter 'FileRetentionDebugXevent', 'True'  
  
```  
  
 下列範例啟用錯誤和警告的電子郵件通知，並設定傳送通知的目的地電子郵件 ID：  
  
```  
Use msdb  
Go  
EXEC managed_backup.sp_set_parameter @parameter_name = 'SSMBackup2WANotificationEmailIds', @parameter_value = '<email address>'  
  
```  
  
  
