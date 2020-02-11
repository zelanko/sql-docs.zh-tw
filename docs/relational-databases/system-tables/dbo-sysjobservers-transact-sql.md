---
title: dbo. sysjobservers （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 08/26/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysjobservers
- sysjobservers_TSQL
- dbo.sysjobservers
- dbo.sysjobservers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysjobservers system table
ms.assetid: 9abcc20f-a421-4591-affb-62674d04575e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 03a4457cb5dd087639a439e9e9bb883eaf924366
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "70026199"
---
# <a name="dbosysjobservers-transact-sql"></a>dbo.sysjobservers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

儲存特定作業與一部或多部目標伺服器的關聯或關係。 這份資料表儲存在 msdb 資料庫中。
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|job_id|**uniqueidentifier**|作業識別碼。|  
|server_id|**int**|伺服器識別碼。|  
|last_run_outcome|**tinyint**|作業上次執行的結果：<br /><br /> **0** = 失敗<br /><br /> **1** = 成功<br /><br /> **2** = 重試<br /><br /> **3** = 取消<br /><br /> **4** = 進行中<br /><br /> **5** = 未知（請參閱下列備註一節） |  
|last_outcome_ message|**nvarchar(1024)**|關聯的訊息 (如果有的話)，包含 last_run_outcome 資料行。|  
|last_run_date|**int**|上次執行作業的日期。|  
|last_run_time|**int**|前次執行作業的時間。|  
|last_run_duration|**int**|此作業執行的持續時間 (以時、分和秒為單位)。 使用公式來計算：（*小時*\*10000） + （*分鐘*\*100） +*秒*。|  


## <a name="remarks"></a>備註

大於*4*的值表示 SQL 代理程式不知道該作業的狀態。 建立作業時， *last_run_outcome*一開始會設為*5* 。


## <a name="see-also"></a>另請參閱

[SQL Server Agent 資料表 &#40;Transact-sql&#41;](../../relational-databases/system-tables/sql-server-agent-tables-transact-sql.md)  
