---
description: 'managed_backup sp_get_backup_diagnostics (Transact-sql) '
title: managed_backup sp_get_backup_diagnostics (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: efd884b6e757ab81cf01eda00b0322ef3ec5c701
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543683"
---
# <a name="managed_backupsp_get_backup_diagnostics-transact-sql"></a>managed_backup sp_get_backup_diagnostics (Transact-sql) 
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  傳回 Smart Admin 記錄的擴充事件。  
  
 使用這個預存程式來監視智慧型系統管理員所記錄的擴充事件。 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 事件會記錄在此系統中，並且可以使用這個預存程式來進行審核和監視。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```sql  
managed_backup.sp_get_backup_diagnostics [@xevent_channel = ] 'event type' [, [@begin_time = ] 'time1' ] [, [@end_time = ] 'time2'VARCHAR(255) = 'Xevent',@begin_time DATETIME = NULL,@end_time DATETIME = NULL  
```  
  
##  <a name="arguments"></a><a name="Arguments"></a> 引數  
 @xevent_channel  
 擴充事件類型。 預設值會設定為傳回過去 30 分鐘內記錄的所有事件。 記錄的事件會視啟用的擴充事件類型而定。 您可以使用此參數篩選預存程序，僅顯示特定類型的事件。 您可以指定完整的事件名稱，或指定子字串，例如： **' admin**'、 **' analytics '**、 **' Operational '** 和 **' Debug '**。 @event_channel是**VARCHAR (255) **。  
  
 若要取得目前已啟用的事件種類清單，請使用 **managed_backup. fn_get_current_xevent_settings** 函數。  
  
 [@begin_time  
 應顯示事件這段期間的起始時間點。 @begin_time參數為 DATETIME，預設值為 Null。 如果未指定此參數，則會顯示過去 30 分鐘的事件。  
  
 @end_time  
 應顯示事件這段期間的結束時間點。 @end_time參數是 DATATIME，預設值是 Null。  如果未指定此參數，則會顯示截至目前時間為止的事件。  
  
## <a name="table-returned"></a>傳回的資料表  
 此預存程序會傳回內含下列資訊的資料表：  
  
| 資料行名稱 | 資料類型 | 描述 |  
| ----------- | --------- | ----------- |
|event_type|NVARCHAR (512) |擴充事件類型。|  
|事件|NVARCHAR (512) |事件記錄的摘要。|  
|時間戳記|timestamp|顯示事件引發時間的事件時間戳記。|  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>權限  
 需要預存程式的 **EXECUTE** 許可權。 它也需要 **VIEW SERVER STATE** 許可權，因為它會在內部呼叫其他需要此許可權的系統物件。  
  
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
  
  
