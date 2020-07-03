---
title: dbo. cdc_jobs （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- cdc_jobs
- cdc_jobs_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dbo.cdc_jobs
ms.assetid: 85e2d580-1c54-4b81-b7e6-2e12997199fd
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c58db6883eb313b65580a1fe4f44b2c2e3b5a3b1
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85890550"
---
# <a name="dbocdc_jobs-transact-sql"></a>dbo.cdc_jobs (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  儲存擷取和清除作業的異動資料擷取組態參數。 此資料表會儲存在**msdb**中。  
  
 
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|在其中執行作業之資料庫的識別碼。|  
|**job_type**|**Nvarchar （20）**|作業的類型：「擷取」或「清除」。|  
|**job_id**|**uniqueidentifier**|與作業相關聯的唯一識別碼。|  
|**maxtrans**|**int**|每個掃描循環中要處理的交易數目上限。<br /><br /> **maxtrans**只對 capture 作業有效。|  
|**maxscans**|**int**|要執行以便從記錄中擷取所有資料列的掃描循環數目上限。<br /><br /> **maxscans**只對 capture 作業有效。|  
|**系列**|**bit**|旗標，指出擷取作業是連續執行 (1)，還是僅執行一次 (0)。 如需詳細資訊，請參閱[sp_cdc_add_job &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md)。<br /><br /> 「**連續**」只對「捕獲」作業有效。|  
|**pollinginterval**|**bigint**|記錄掃描循環之間的秒數。<br /><br /> **pollinginterval**只對 capture 作業有效。|  
|**保存**|**bigint**|變更資料列要保留在變更資料表中的分鐘數。<br /><br /> **保留**僅適用于清除作業。|  
|**threshold**|**bigint**|可以使用單一清除陳述式來刪除的最大刪除項目數。|  
  
## <a name="see-also"></a>另請參閱  
 [sp_cdc_add_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md)   
 [sp_cdc_change_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-change-job-transact-sql.md)   
 [sp_cdc_help_jobs &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql.md)   
 [sp_cdc_drop_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-drop-job-transact-sql.md)  
  
  
