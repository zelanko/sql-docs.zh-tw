---
title: managed_backup. fn_get_health_status (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_get_health_status_TSQL
- smart_admin.fn_get_health_status_TSQL
- smart_admin.fn_get_health_status
- fn_get_health_status
dev_langs:
- TSQL
helpviewer_keywords:
- smart_admin.fn_get_health_status
- fn_get_health_status
ms.assetid: b376711d-444a-4b5e-b483-8df323b4e31f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: bc2bfdbd8714bf4211373e921c1b054ed224feb3
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155808"
---
# <a name="managed_backupfn_get_health_status-transact-sql"></a>managed_backup.fn_get_health_status & Amp;&#40;transact-SQL&AMP;&#41;
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  傳回擴充事件針對一段指定期間所報告，包含 0 個、一個或多個彙總錯誤計數資料列的資料表。  
  
 函式可用來回報 [Smart Admin] 底下服務的健全狀況狀態。目前[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]在智慧型系統管理傘下受到支援。 因此傳回的錯誤與[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]相關。  
  
 
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```sql  
managed_backup.fn_get_health_status([@begin_time = ] 'time_1' , [ @end_time = ] 'time_2')  
```  
  
##  <a name="Arguments"></a> 引數  
 [@begin_time]  
 彙總的錯誤計數開始計算的期間。  @begin_time參數為 DATETIME。 預設值是 NULL。 當值為 NULL 時，函數將處理最早在目前時間的過去 30 分鐘內報告的事件。  
  
 [ @end_time]  
 彙總的錯誤計數結束計算的期間。 @end_time參數為 DATETIME, 預設值為 Null。 當值為 NULL 時，函數將處理截至目前時間為止的擴充事件。  
  
## <a name="table-returned"></a>傳回的資料表  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|number_of_storage_connectivity_errors|ssNoversion|程式連線到 Azure 儲存體帳戶時的連接錯誤數目。|  
|number_of_sql_errors|ssNoversion|程式連接到 SQL Server 引擎時傳回的錯誤數目。|  
|number_of_invalid_credential_errors|ssNoversion|程式嘗試使用 SQL 認證進行驗證時傳回的錯誤數目。|  
|number_of_other_errors|ssNoversion|除了連接、SQL 或認證以外其他類別目錄中的錯誤數目。|  
|number_of_corrupted_or_deleted_backups|ssNoversion|已刪除或損毀的備份檔案數目。|  
|number_of_backup_loops|ssNoversion|備份代理程式掃描[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]所設定的全部資料庫的次數。|  
|number_of_retention_loops|ssNoversion|掃描資料庫以評估所設定保留週期的次數。|  
  
## <a name="best-practices"></a>最佳作法  
 這些彙總計算可用來監視系統健全狀況。 例如，如果 number_of_retention_loops 資料行在 30 分鐘內為 0，則保留管理可能需要耗費長時間運作，或甚至運作不正確。 非零的錯誤資料行可能表示出現問題，應檢查擴充事件記錄來了解任何問題。 或者, 使用預存程式**managed_backup**來取得擴充事件的清單, 以找出錯誤的詳細資料。  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>Permissions  
 需要函數的**SELECT**許可權。  
  
## <a name="examples"></a>範例  
  
-   下列範例會傳回從執行的時間起算，過去 30 分鐘內的彙總錯誤計數。  
  
    ```  
    SELECT *  
    FROM managed_backup.fn_get_health_status(NULL, NULL)  
  
    ```  
  
-   下列範例會傳回本星期的彙總錯誤計數：  
  
    ```  
    Use msdb  
    Go  
    DECLARE @startofweek datetime  
    DECLARE @endofweek datetime  
    SET @startofweek = DATEADD(Day, 1-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)   
    SET @endofweek = DATEADD(Day, 7-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)  
    SELECT *  
    FROM managed_backup.fn_get_health_status(@startofweek, @endofweek)  
  
    ```  
  
  
