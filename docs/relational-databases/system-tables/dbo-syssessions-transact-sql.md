---
title: dbo.syssessions (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dbo.syssessions_TSQL
- dbo.syssessions
- syssessions_TSQL
- syssessions
dev_langs:
- TSQL
helpviewer_keywords:
- syssessions system table
ms.assetid: 187819b6-c7f4-4a26-b74c-0a89e96695cf
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3099413685b594404a577d71011bb1738b756ac1
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="dbosyssessions-transact-sql"></a>dbo.syssessions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  每次啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 時，它都會建立新的工作階段。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 利用工作階段來保留 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務非預期地重新啟動或停止時的作業狀態。 每個資料列的**syssessions**資料表包含約一個工作階段的資訊。 使用**sysjobactivity**資料表以檢視工作狀態，每個工作階段的結尾。  
  
 這份資料表儲存在**msdb**資料庫。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 工作階段的識別碼。|  
|**agent_start_date**|**datetime**|啟動這個工作階段的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務的日期和時間。|  
  
## <a name="remarks"></a>備註  
 成員之使用者的**sysadmin**固定的伺服器角色可以存取這份資料表。  
  
## <a name="see-also"></a>另請參閱  
 [dbo.sysjobactivity &#40;TRANSACT-SQL &#41;](../../relational-databases/system-tables/dbo-sysjobactivity-transact-sql.md)  
  
  
