---
title: dbo.systargetservers (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dbo.systargetservers_TSQL
- dbo.systargetservers
- systargetservers_TSQL
- systargetservers
dev_langs:
- TSQL
helpviewer_keywords:
- systargetservers system table
ms.assetid: 479d1314-be37-4d19-ac9c-419fc9110e53
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1fcce3f0020036cc0a0d21021be24dcdcd8ab19a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="dbosystargetservers-transact-sql"></a>dbo.systargetservers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  記錄在這個多伺服器的作業網域中，目前編列了哪些目標伺服器。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**server_id**|**int**|伺服器識別碼。|  
|**server_name**|**sysname**|伺服器名稱。|  
|**location**|**nvarchar(200)**|指定之目標伺服器的位置。|  
|**time_zone_adjustment**|**int**|相對於格林威治標準時間 (GMT) 的時間調整間隔 (小時)。|  
|**enlist_date**|**datetime**|編列指定的目標伺服器之日期和時間。|  
|**last_poll_date**|**datetime**|指定的目標伺服器上次輪詢多伺服器的日期和時間**sysdownloadlist**要執行之工作的系統資料表。|  
|**status**|**int**|目標伺服器的狀態：<br /><br /> **1** = 正常<br /><br /> **2** = 暫止的重新同步處理<br /><br /> **4** = 可能離線|  
|**local_time_at_last_poll**|**datetime**|前次輪詢目標伺服器來尋找作業的日期和時間。|  
|**enlisted_by_nt_user**|**nvarchar(100)**|執行之人員的使用者名稱**sp_msx_enlist**目標伺服器上。|  
|**poll_internal**|**int**|目標伺服器經過多久 (秒) 之後，便輪詢主要伺服器來尋找新的下載指示。|  
  
  
