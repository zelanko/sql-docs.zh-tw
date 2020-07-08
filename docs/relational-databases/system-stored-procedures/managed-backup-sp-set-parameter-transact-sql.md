---
title: managed_backup. sp_set_parameter （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 3eab417e1d959c990e53aca3119546a73a3e1aad
ms.sourcegitcommit: 703968b86a111111a82ef66bb7467dbf68126051
ms.contentlocale: zh-TW
ms.lasthandoff: 07/07/2020
ms.locfileid: "86052910"
---
# <a name="managed_backupsp_set_parameter-transact-sql"></a>managed_backup. sp_set_parameter （Transact-sql）
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  設定指定的 Smart Admin 系統參數值。  
  
 可用的參數與[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]相關。 這些參數可用來設定電子郵件通知、啟用特定擴充事件，以及啟用使用者設定原則式管理原則。 您必須指定參數名稱與參數值組。  

  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```sql  
EXEC managed_backup.sp_set_parameter   
    [@parameter_name = ] {'SSMBackup2WANotificationEmailIds' | 'SSMBackup2WAEnableUserDefinedPolicy' | 'SSMBackup2WADebugXevent' | 'FileRetentionDebugXevent' | 'StorageOperationDebugXevent'}  
    ,[@parameter_value = ] 'parameter_value'  
```  
  
##  <a name="arguments"></a><a name="Arguments"></a>參量  
 @parameter_name  
 您要設定值之參數的名稱。 @parameter_name為 NVARCHAR （128）。 可用的參數名稱為**SSMBackup2WANotificationEmailIds**、 **SSMBackup2WADebugXevent**、 **SSMBackup2WAEnableUserDefinedPolicy**、 **FileRetentionDebugXevent**和**StorageOperationDebugXevent**。  
  
 @parameter_value  
 您要設定之參數的值。 @parameter值為 NVARCHAR （128）。  以下是允許的參數名稱與值組：  
  
-   @parameter_name= ' SSMBackup2WANotificationEmailIds '： @parameter_value = ' email '  
  
-   @parameter_name= ' SSMBackup2WAEnableUserDefinedPolicy '： @parameter_value = {' true ' |' false '}  
  
-   @parameter_name= ' SSMBackup2WADebugXevent '： @parameter_value = {' true ' |' false '}  
  
-   @parameter_name= ' FileRetentionDebugXevent '： @parameter_value = {' true ' |' false '}  
  
-   @parameter_name= ' StorageOperationDebugXevent ' = {' true ' |' false '}  
  
## <a name="return-code-value"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="best-practices"></a>最佳做法  
 描述使用者執行陳述式或常式時應了解之最佳作法的選用章節。  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>權限  
 需要 managed_backup 上的**EXECUTE**許可權**sp_set_parameter**預存程式。  
  
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
  
  
