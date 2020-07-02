---
title: dbo.sys會話（Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 12/30/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 91da4b73125c61f23d027bf99d2550a1d449a7a1
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85750263"
---
# <a name="dbosyssessions-transact-sql"></a>dbo.syssessions (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

每次啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 時，它都會建立新的工作階段。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 利用工作階段來保留 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務非預期地重新啟動或停止時的作業狀態。 **Syssessions**資料表的每個資料列都包含一個會話的相關資訊。 使用**sysjobactivity**資料表來查看每個會話結束時的作業狀態。  
  
 此資料表會儲存在**msdb**資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 工作階段的識別碼。 這個 session_id 不是會話的 SPID，而是此系統資料表中的識別值。|  
|**agent_start_date**|**datetime**|啟動這個工作階段的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務的日期和時間。|  
  
## <a name="remarks"></a>備註  
 只有身為**系統管理員（sysadmin** ）固定伺服器角色成員的使用者，才能夠存取此資料表。  
  
## <a name="see-also"></a>另請參閱  
 [dbo.sysjobactivity &#40;Transact-sql&#41;](../../relational-databases/system-tables/dbo-sysjobactivity-transact-sql.md)  
  
  
