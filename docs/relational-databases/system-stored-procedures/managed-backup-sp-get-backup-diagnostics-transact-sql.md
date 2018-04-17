---
title: managed_backup.sp_get_backup_diagnostics (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_get_backup_diagnostics_TSQL
- sp_get_backup_diagnostics
- smart_admin.sp_get_backup_diagnostics_TSQL
- smart_admin.sp_get_backup_diagnostics
dev_langs:
- TSQL
helpviewer_keywords:
- sp_get_backup_diagnostics
- smart_admin.sp_get_backup_diagnostics
ms.assetid: 2266a233-6354-464b-91ec-824ca4eb9ceb
caps.latest.revision: 12
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fc8d877b260a86cb3d00b132813ccea62c34f17f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="managedbackupspgetbackupdiagnostics-transact-sql"></a>managed_backup.sp_get_backup_diagnostics (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  傳回 Smart Admin 記錄的擴充事件。  
  
 使用此預存程序來監視 Smart admin 記錄的擴充事件[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]事件會記錄在此系統，可以檢閱和使用這個預存程序監視。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```sql  
managed_backup.sp_get_backup_diagnostics [@xevent_channel = ] 'event type' [, [@begin_time = ] 'time1' ] [, [@end_time = ] 'time2'VARCHAR(255) = 'Xevent',@begin_time DATETIME = NULL,@end_time DATETIME = NULL  
```  
  
##  <a name="Arguments"></a> 引數  
 @xevent_channel  
 擴充事件類型。 預設值會設定為傳回過去 30 分鐘內記錄的所有事件。 記錄的事件會視啟用的擴充事件類型而定。 您可以使用此參數篩選預存程序，僅顯示特定類型的事件。 您可以指定完整事件名稱，或指定子字串，例如： **'Admin'**， **'Analytic'**， **'Operational'**，和**'Debug'**. @event_channel是**VARCHAR (255)**。  
  
 若要取得事件類型目前已啟用，請使用清單**managed_backup.fn_get_current_xevent_settings**函式。  
  
 [@begin_time  
 應顯示事件這段期間的起始時間點。 @begin_time參數為 DATETIME，預設值是 NULL。 如果未指定此參數，則會顯示過去 30 分鐘的事件。  
  
 @end_time  
 應顯示事件這段期間的結束時間點。 @end_time參數為 DATATIME，其預設值是 NULL。  如果未指定此參數，則會顯示截至目前時間為止的事件。  
  
## <a name="table-returned"></a>傳回的資料表  
 此預存程序會傳回內含下列資訊的資料表：  
  
||||  
|-|-|-|  
|資料行名稱|資料類型|Description|  
|event_type|NVARCHAR(512)|擴充事件類型。|  
|事件|NVARCHAR(512)|事件記錄的摘要。|  
|時間戳記|TIMESTAMP|顯示事件引發時間的事件時間戳記。|  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>Permissions  
 需要**EXECUTE**預存程序的權限。 它也需要**VIEW SERVER STATE**權限，因為它在內部呼叫其他系統物件，需要此權限。  
  
## <a name="examples"></a>範例  
 下列範例傳回過去 30 分鐘內記錄的所有事件。  
  
```  
Use msdb  
Go  
EXEC managed_backup.sp_get_backup_diagnostics  
  
```  
  
 下列範例傳回特定時間範圍內記錄的所有事件。  
  
```  
Use msdb  
Go  
EXEC managed_backup.sp_get_backup_diagnostics @xevent_channel = 'Admin',  
  @begin_time = '2013-06-01', @end_time = '2013-06-10'  
  
```  
  
 下列範例傳回過去 30 分鐘內記錄的所有分析事件。  
  
```  
Use msdb  
Go  
EXEC managed_backup.sp_get_backup_diagnostics @xevent_channel = 'Analytic'  
  
```  
  
  
