---
title: "managed_backup.sp_backup_on_demand (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
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
- smart_admin.sp_backup_on_demand
- smart_admin.sp_backup_on_demand_TSQL
- sp_backup_on_demand_TSQL
- sp_backup_on_demand
dev_langs: TSQL
helpviewer_keywords:
- smart_admin.sp_backup_on_demand
- sp_backup_on_demand
ms.assetid: 638f809f-27fa-4c44-a549-9cf37ecc920c
caps.latest.revision: "13"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2f57ab46aee2ab6784179fa495d96afb45c3751d
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="managedbackupspbackupondemand-transact-sql"></a>managed_backup.sp_backup_on_demand (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  要求[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]執行指定資料庫的備份。  
  
 使用此預存程序可執行以[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]設定之資料庫的隨選備份。 如此可防止任何備份鏈結中斷、感知[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]程序，且備份會儲存在相同的 Windows Azure Blob 儲存體容器中。  
  
 成功完成備份時，會傳回完整備份檔案路徑。 此路徑包含備份作業所產生之新備份檔案的名稱和位置。  
  
 如果 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 正在執行指定資料庫的給定類型備份，則會傳回錯誤。 在此情況下，傳回的錯誤訊息會包含目前備份上傳目的地的完整備份檔案路徑。  
   
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```tsql  
EXEC managed_backup.sp_backup_on_demand   
[@database_name  =]  'database name',[@type = ] { 'Database' | 'Log' }  
  
```  
  
##  <a name="Arguments"></a> 引數  
 @database_name  
 執行備份所在之資料庫的名稱。 @database_name是**SYSNAME**。  
  
 @type  
 要執行的備份類型：資料庫或記錄。 @type參數是**nvarchar （32)**。  
  
## <a name="return-code-value"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>Permissions  
 需要的成員資格**db_backupoperator**與資料庫角色， **ALTER ANY CREDENTIAL**權限，和**EXECUTE**權限**sp_delete_backuphistory**預存程序。  
  
## <a name="examples"></a>範例  
 下列範例提出資料庫 'TestDB' 的資料庫備份要求。 此資料庫已啟用[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]。  
  
```  
Use MSDB  
Go  
EXEC managed_backup.sp_backup_on_demand  
 @database_name = 'TestDB'  
,@type = 'Database'  
  
```  
  
 針對每個程式碼片段，請在語言屬性欄位中選取 'tsql'。  
  
  
