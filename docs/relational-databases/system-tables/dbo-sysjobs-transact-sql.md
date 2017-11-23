---
title: "dbo.sysjobs (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysjobs
- sysjobs_TSQL
- dbo.sysjobs
- dbo.sysjobs_TSQL
dev_langs: TSQL
helpviewer_keywords: sysjobs system table
ms.assetid: e244a6a5-54c2-47a6-8039-dd1852b0ae59
caps.latest.revision: "17"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 1fd6e90a9e823e38a83f5b218027e15183ab76ae
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="dbosysjobs-transact-sql"></a>dbo.sysjobs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  儲存 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 所要執行之各項排程作業的資訊。 這份資料表儲存在**msdb**資料庫。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**job_id**|**uniqueidentifier**|作業的唯一識別碼。|  
|**originating_server_id**|**int**|作業的來源伺服器識別碼。|  
|**name**|**sysname**|作業名稱。|  
|**已啟用**|**tinyint**|指出是否啟用作業，以便執行。|  
|**描述**|**nvarchar(512)**|作業的描述。|  
|**start_step_id**|**int**|應該作為執行起點的作業步驟識別碼。|  
|**category_id**|**int**|作業類別目錄的識別碼。|  
|**owner_sid**|**varbinary(85)**|作業擁有者的安全性識別碼 (SID)。|  
|**notify_level_eventlog**|**int**|**位元遮罩**指出在哪些情況之下應該將通知事件記錄到 Microsoft Windows 應用程式記錄檔：<br /><br /> **0** = 永不<br /><br /> **1** = 當作業成功時<br /><br /> **2** = 當作業失敗<br /><br /> **3** = 每當作業完成 （不論作業結果）|  
|**notify_level_email**|**int**|這是一個位元組遮罩，指出在哪些情況之下，應該在作業完成時傳送通知電子郵件：<br /><br /> **0** = 永不<br /><br /> **1** = 當作業成功時<br /><br /> **2** = 當作業失敗<br /><br /> **3** = 每當作業完成 （不論作業結果）|  
|**notify_level_netsend**|**int**|這是一個位元組遮罩，指出在哪些情況之下，應該在作業完成時傳送網路訊息：<br /><br /> **0** = 永不<br /><br /> **1** = 當作業成功時<br /><br /> **2** = 當作業失敗<br /><br /> **3** = 每當作業完成 （不論作業結果）|  
|**notify_level_page**|**int**|這是一個位元組遮罩，指出在哪些情況之下，應該在作業完成時傳送頁面：<br /><br /> **0** = 永不<br /><br /> **1** = 當作業成功時<br /><br /> **2** = 當作業失敗<br /><br /> **3** = 每當作業完成 （不論作業結果）|  
|**notify_email_operator_id**|**int**|要通知的操作員電子郵件名稱。|  
|**notify_netsend_operator_id**|**int**|傳送網路訊息時所用的電腦或使用者識別碼。|  
|**notify_page_operator_id**|**int**|傳送呼叫時所用的電腦或使用者識別碼。|  
|**delete_level**|**int**|**位元遮罩**指出在哪些情況之下，應該刪除作業在作業完成時：<br /><br /> **0** = 永不<br /><br /> **1** = 當作業成功時<br /><br /> **2** = 當作業失敗<br /><br /> **3** = 每當作業完成 （不論作業結果）|  
|**date_created**|**datetime**|作業的建立日期。|  
|**date_modified**|**datetime**|上次修改作業的日期。|  
|**version_number**|**int**|作業的版本。|  
  
  
