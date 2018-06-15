---
title: logmarkhistory (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- logmarkhistory
- logmarkhistory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- logmarkhistory system table
ms.assetid: 5c1becc5-f34e-4869-bf69-dfafab684540
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c3498368a2c38f5e1c64d38c26920a7a9a9b5e1f
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
ms.locfileid: "33258318"
---
# <a name="logmarkhistory-transact-sql"></a>logmarkhistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對已認可的每個標示交易，各包含一個資料列。 這份資料表儲存在**msdb**資料庫。  
  

|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**database_name**|**nvarchar(128)**|發生標示的交易之本機資料庫。|  
|**mark_name**|**nvarchar(128)**|使用者提供的標示交易名稱。|  
|**描述**|**nvarchar(255)**|使用者提供的標示交易描述。 可以是 NULL。|  
|**user_name**|**nvarchar(128)**|執行標示交易的資料庫使用者名稱。 可以是 NULL。|  
|**lsn**|**numeric(25,0)**|標示所在之交易記錄的記錄序號。|  
|**mark_time**|**datetime**|標示的交易之認可時間 (本機時間)。|  
  
## <a name="see-also"></a>另請參閱  
 [還原資料庫至標示的交易 &#40;SQL Server Management Studio&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)   
 [使用標示的異動以一致的方式復原相關資料庫 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md)   
 [系統資料表 &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
