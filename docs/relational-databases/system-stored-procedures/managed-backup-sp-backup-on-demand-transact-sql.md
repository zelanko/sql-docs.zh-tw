---
title: managed_backup. sp_backup_on_demand （Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: e34cf20585ea7dcd3690d80ee415fc274bf852ca
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "70155394"
---
# <a name="managed_backupsp_backup_on_demand-transact-sql"></a>managed_backup. sp_backup_on_demand （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  要求[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]執行指定資料庫的備份。  
  
 使用此預存程序可執行以[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]設定之資料庫的隨選備份。 這可防止備份鏈和[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]進程中的任何中斷，並將備份儲存在相同的 Azure Blob 儲存體容器中。  
  
 成功完成備份時，會傳回完整備份檔案路徑。 此路徑包含備份作業所產生之新備份檔案的名稱和位置。  
  
 如果 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 正在執行指定資料庫的給定類型備份，則會傳回錯誤。 在此情況下，傳回的錯誤訊息會包含目前備份上傳目的地的完整備份檔案路徑。  
   
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```sql  
EXEC managed_backup.sp_backup_on_demand   
[@database_name  =]  'database name',[@type = ] { 'Database' | 'Log' }  
  
```  
  
##  <a name="arguments"></a><a name="Arguments"></a>參量  
 @database_name  
 執行備份所在之資料庫的名稱。 @database_name為**SYSNAME**。  
  
 @type  
 要執行的備份類型：資料庫或記錄。 @type參數是**NVARCHAR （32）**。  
  
## <a name="return-code-value"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>權限  
 需要**db_backupoperator**資料庫角色中的成員資格、具有**ALTER ANY CREDENTIAL**許可權，以及**Sp_delete_backuphistory**預存程式的**EXECUTE**許可權。  
  
## <a name="examples"></a>範例  
 下列範例會建立資料庫 ' TestDB ' 的資料庫備份要求。 此資料庫已啟用[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]。  
  
```  
Use MSDB  
Go  
EXEC managed_backup.sp_backup_on_demand  
 @database_name = 'TestDB'  
,@type = 'Database'  
  
```  
  
 針對每個程式碼片段，請在語言屬性欄位中選取 'tsql'。  
  
  
