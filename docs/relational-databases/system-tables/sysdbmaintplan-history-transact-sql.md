---
title: "sysdbmaintplan_history (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
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
- sysdbmaintplan_history_TSQL
- sysdbmaintplan_history
dev_langs: TSQL
helpviewer_keywords: sysdbmaintplan_history system table
ms.assetid: 02d36f08-ac93-4463-bb59-284c5cd6ed04
caps.latest.revision: "29"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5407585f3ff226234a114cdbf14036422b487580
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="sysdbmaintplanhistory-transact-sql"></a>sysdbmaintplan_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  這份資料表儲存在**msdb**資料庫。  
  
 [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)]  
  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**sequence_id**|**int**|資料庫維護計畫執行記錄的順序。|  
|**plan_id**|**uniqueidentifier**|資料庫維護計畫識別碼。|  
|**plan_name**|**sysname**|資料庫維護計畫名稱。|  
|**database_name**|**sysname**|資料庫維護計畫之相關資料庫的名稱。|  
|**伺服器名稱**|**sysname**|系統名稱。|  
|**活動**|**nvarchar （128)**|資料庫維護計畫所執行的活動 (如備份交易記錄等)。|  
|**succeeded**|**bit**|**0** = 成功**1** = 失敗|  
|**end_time**|**datetime**|動作完成的時間。|  
|**duration**|**int**|完成資料庫維護計畫動作所需要的時間長度。|  
|**start_time**|**datetime**|動作開始的時間。|  
|**error_number**|**int**|失敗時所報告的錯誤號碼。|  
|**訊息**|**nvarchar(512)**|所產生的訊息**sqlmaint**。|  
  
  
