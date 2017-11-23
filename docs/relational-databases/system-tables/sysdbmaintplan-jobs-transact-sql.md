---
title: "sysdbmaintplan_jobs (TRANSACT-SQL) |Microsoft 文件"
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
- sysdbmaintplan_jobs
- sysdbmaintplan_jobs_TSQL
dev_langs: TSQL
helpviewer_keywords: sysdbmaintplan_jobs system table
ms.assetid: bc65cd70-6ef2-4c17-be11-877ecf4efe50
caps.latest.revision: "28"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a10398311460d0e002c8adf059a1887c7d0d81af
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="sysdbmaintplanjobs-transact-sql"></a>sysdbmaintplan_jobs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  這個資料表會包含在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，以保存從舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 升級而來之執行個體的現有資訊。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不會變更此資料表的內容。 這份資料表儲存在**msdb**資料庫。  
  
 [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)]  
  

  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**plan_id**|**uniqueidentifier**|資料庫維護計畫識別碼。|  
|**job_id**|**uniqueidentifier**|資料庫維護計畫之相關作業的識別碼。|  
  
  
