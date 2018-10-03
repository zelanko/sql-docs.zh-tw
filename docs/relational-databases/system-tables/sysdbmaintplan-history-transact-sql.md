---
title: sysdbmaintplan_history (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdbmaintplan_history_TSQL
- sysdbmaintplan_history
dev_langs:
- TSQL
helpviewer_keywords:
- sysdbmaintplan_history system table
ms.assetid: 02d36f08-ac93-4463-bb59-284c5cd6ed04
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a51e2ea16ab7cc34ade122284a7162707c4d8f7d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47732666"
---
# <a name="sysdbmaintplanhistory-transact-sql"></a>sysdbmaintplan_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  這份資料表儲存在**msdb**資料庫。  
  
 [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)]  
  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**sequence_id**|**int**|資料庫維護計畫執行記錄的順序。|  
|**plan_id**|**uniqueidentifier**|資料庫維護計畫識別碼。|  
|**plan_name**|**sysname**|資料庫維護計畫名稱。|  
|**database_name**|**sysname**|資料庫維護計畫之相關資料庫的名稱。|  
|**server_name**|**sysname**|系統名稱。|  
|**活動**|**nvarchar(128)**|資料庫維護計畫所執行的活動 (如備份交易記錄等)。|  
|**succeeded**|**bit**|**0** = 成功**1** = 失敗|  
|**end_time**|**datetime**|動作完成的時間。|  
|**duration**|**int**|完成資料庫維護計畫動作所需要的時間長度。|  
|**start_time**|**datetime**|動作開始的時間。|  
|**error_number**|**int**|失敗時所報告的錯誤號碼。|  
|**message**|**nvarchar(512)**|所產生的訊息**sqlmaint**。|  
  
  
