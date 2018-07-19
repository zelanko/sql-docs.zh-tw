---
title: dbo.sysproxysubsystem (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 13
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1d1b9a2dc37075ca09d31aaa3faf46149f17fe93
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
ms.locfileid: "33254733"
---
# <a name="dbosysproxysubsystem-transact-sql"></a>dbo.sysproxysubsystem (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  記錄每個 Proxy 帳戶使用哪個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 子系統。 這份資料表儲存在**msdb**資料庫。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**subsystem_id**|**int**|子系統的識別碼。 這個值會對應到**syssubsystems**中的資料行**syssubsystems**資料表。|  
|**proxy_id**|**int**|Proxy 帳戶的識別碼。 這個值會對應到**proxy_id**中的資料行**sysproxies**資料表。|  
  
## <a name="remarks"></a>備註  
 只有成員**sysadmin**固定的伺服器角色可以存取這份資料表。  
  
## <a name="see-also"></a>另請參閱  
 [dbo.syssubsystems &#40;Transact SQL&#41;](../../relational-databases/system-tables/dbo-syssubsystems-transact-sql.md)   
 [dbo.sysproxies &#40;Transact SQL&#41;](../../relational-databases/system-tables/dbo-sysproxies-transact-sql.md)  
  
  
