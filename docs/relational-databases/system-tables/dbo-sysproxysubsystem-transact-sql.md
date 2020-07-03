---
title: dbo.sysproxysubsystem （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysproxysubsystem_TSQL
- dbo.sysproxysubsystem
- sysproxysubsystem_TSQL
- sysproxysubsystem
dev_langs:
- TSQL
helpviewer_keywords:
- sysproxysubsystem system table
ms.assetid: 6d7713f5-1253-4a19-b1fb-635c377c95c1
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 287cd7113fe416f59bfe4351cebd2aee59b17832
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85890405"
---
# <a name="dbosysproxysubsystem-transact-sql"></a>dbo.sysproxysubsystem (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  記錄每個 Proxy 帳戶使用哪個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 子系統。 此資料表會儲存在**msdb**資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**subsystem_id**|**int**|子系統的識別碼。 這個值會對應至**syssubsystems**資料表中的**subsystem_id**資料行。|  
|**proxy_id**|**int**|Proxy 帳戶的識別碼。 這個值會對應至**sysproxies**資料表中的**proxy_id**資料行。|  
  
## <a name="remarks"></a>備註  
 只有**系統管理員（sysadmin** ）固定伺服器角色的成員，才能夠存取此資料表。  
  
## <a name="see-also"></a>另請參閱  
 [dbo.sys子系統 &#40;Transact-sql&#41;](../../relational-databases/system-tables/dbo-syssubsystems-transact-sql.md)   
 [dbo.sysproxy &#40;Transact-sql&#41;](../../relational-databases/system-tables/dbo-sysproxies-transact-sql.md)  
  
  
