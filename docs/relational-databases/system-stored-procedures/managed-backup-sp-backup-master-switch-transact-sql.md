---
title: managed_backup. sp_backup_master_switch （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_ backup_master_switch
- smart_admin.sp_backup_master_switch
- sp_ backup_master_switch_TSQL
- smart_admin.sp_backup_master_switch_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_ backup_master_switch
- smart_admin.sp_backup_master_switch
ms.assetid: 1ed2b2b2-c897-41cc-bed5-1c6bc47b9dd2
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: eb140e5ff831373d2725bca82c70655c5745a658
ms.sourcegitcommit: 703968b86a111111a82ef66bb7467dbf68126051
ms.contentlocale: zh-TW
ms.lasthandoff: 07/07/2020
ms.locfileid: "86053534"
---
# <a name="managed_backupsp_backup_master_switch-transact-sql"></a>managed_backup. sp_backup_master_switch （Transact-sql）
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  暫停或繼續執行[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]。  
  
 使用此預存程序可暫停再繼續執行[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]。 如此可確保所有組態設定都會留下，並在作業繼續執行時保留。 暫停[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]時，不會強制執行保留期間。 這表示，不會檢查並判斷是否應該從儲存體中刪除檔案，或者是否發生備份檔案損毀或記錄鏈結中斷的情況。  
  

  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```sql  
EXEC managed_backup.sp_backup_master_switch   
                     [@new_state = ] { 0 | 1}  
```  
  
##  <a name="arguments"></a><a name="Arguments"></a>參量  
 @state  
 設定 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 的狀態。 @state參數為**BIT**。 當值設定為 0 時，作業會暫停；當值設定為 1 時，作業會繼續執行。  
  
## <a name="return-code-value"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="security"></a>安全性  
 描述與陳述式相關的安全性問題。加入＜權限＞小節 (H3 標題)。 考慮加入＜擁有權鏈結＞和＜稽核＞小節 (如果適用)。  
  
### <a name="permissions"></a>權限  
 需要**db_backupoperator**資料庫角色中的成員資格、具有**ALTER ANY CREDENTIAL**許可權，以及**Sp_delete_backuphistory**預存程式的**EXECUTE**許可權。  
  
## <a name="examples"></a>範例  
 下列範例可用來暫停在執行個體上執行的[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]：  
  
```  
Use msdb;  
GO  
EXEC managed_backup.sp_backup_master_switch @new_state=0;  
Go  
  
```  
  
 下列範例可用來繼續執行[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]。  
  
```  
Use msdb;  
GO  
EXEC managed_backup.sp_backup_master_switch @new_state=1;  
Go  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 受控備份到 Microsoft Azure](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)  
  
  
