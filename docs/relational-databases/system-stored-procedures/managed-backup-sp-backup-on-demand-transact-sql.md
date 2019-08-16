---
title: managed_backup.sp_backup_on_demand (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- smart_admin.sp_backup_on_demand
- smart_admin.sp_backup_on_demand_TSQL
- sp_backup_on_demand_TSQL
- sp_backup_on_demand
dev_langs:
- TSQL
helpviewer_keywords:
- smart_admin.sp_backup_on_demand
- sp_backup_on_demand
ms.assetid: 638f809f-27fa-4c44-a549-9cf37ecc920c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 980fb3006819e5727033376beae1f8156d26e0fc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67942056"
---
# <a name="managed_backupsp_backup_on_demand-transact-sql"></a>managed_backup.sp_backup_on_demand & Amp;&#40;transact-SQL&AMP;&#41;
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  要求[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]執行指定資料庫的備份。  
  
 使用此預存程序可執行以[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]設定之資料庫的隨選備份。 如此可防止任何備份鏈結中斷、感知[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]程序，且備份會儲存在相同的 Windows Azure Blob 儲存體容器中。  
  
 成功完成備份時，會傳回完整備份檔案路徑。 此路徑包含備份作業所產生之新備份檔案的名稱和位置。  
  
 如果 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 正在執行指定資料庫的給定類型備份，則會傳回錯誤。 在此情況下，傳回的錯誤訊息會包含目前備份上傳目的地的完整備份檔案路徑。  
   
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```sql  
EXEC managed_backup.sp_backup_on_demand   
[@database_name  =]  'database name',[@type = ] { 'Database' | 'Log' }  
  
```  
  
##  <a name="Arguments"></a> 引數  
 @database_name  
 執行備份所在之資料庫的名稱。 @database_name已 **SYSNAME**。  
  
 @type  
 要執行的備份類型：資料庫或記錄檔。 @type參數是 **NVARCHAR(32)** 。  
  
## <a name="return-code-value"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>Permissions  
 需要的成員資格**db_backupoperator**資料庫角色，使用**ALTER ANY CREDENTIAL**權限，並**EXECUTE**的權限**sp_delete_backuphistory**預存程序。  
  
## <a name="examples"></a>範例  
 下列範例會使資料庫 'TestDB' 的資料庫備份要求。 此資料庫已啟用[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]。  
  
```  
Use MSDB  
Go  
EXEC managed_backup.sp_backup_on_demand  
 @database_name = 'TestDB'  
,@type = 'Database'  
  
```  
  
 針對每個程式碼片段，請在語言屬性欄位中選取 'tsql'。  
  
  
