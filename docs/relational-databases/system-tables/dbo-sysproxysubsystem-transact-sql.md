---
title: dbo.sysproxysubsystem (TRANSACT-SQL) |Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e6fa0ff8c90f4532d87191f827e0815de8636033
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47781616"
---
# <a name="dbosysproxysubsystem-transact-sql"></a>dbo.sysproxysubsystem (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  記錄每個 Proxy 帳戶使用哪個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 子系統。 這份資料表儲存在**msdb**資料庫。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**subsystem_id**|**int**|子系統的識別碼。 這個值會對應到**syssubsystems**中的資料行**syssubsystems**資料表。|  
|**proxy_id**|**int**|Proxy 帳戶的識別碼。 這個值會對應到**proxy_id**中的資料行**sysproxies**資料表。|  
  
## <a name="remarks"></a>備註  
 只有成員**sysadmin**固定的伺服器角色可以存取這份資料表。  
  
## <a name="see-also"></a>另請參閱  
 [dbo.syssubsystems &#40;Transact SQL&#41;](../../relational-databases/system-tables/dbo-syssubsystems-transact-sql.md)   
 [dbo.sysproxies &#40;Transact SQL&#41;](../../relational-databases/system-tables/dbo-sysproxies-transact-sql.md)  
  
  
