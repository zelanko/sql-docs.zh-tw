---
title: M (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSpublisher_databases
- MSpublisher_databases_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpublisher_databases system table
ms.assetid: 59b0166e-a64c-46b8-befc-c222fa1ccce2
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c68799a4e533ea35ab7fc39e1e08817655e97498
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="mspublisherdatabases-transact-sql"></a>MSpublisher_databases (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSpublisher_databases**資料表包含每個發行者/發行者資料庫組本機散發者所服務的一個資料列。 這份資料表儲存在散發資料庫中。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|發行者的識別碼。|  
|**publisher_db**|**sysname**|發行者資料庫的名稱。|  
|**id**|**int**|資料列的識別碼。|  
|**publisher_engine_edition**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者的版本，可以是下列其中一個版本：<br /><br /> **10** = personal Edition<br /><br /> **11** = desktop Engine (MSDE)<br /><br /> **20** = standard<br /><br /> **21** = 工作群組<br /><br /> **30** = Enterprise （評估版）<br /><br /> **31** = 開發人員<br /><br /> **40** = express （Express 不能是發行者。 存在這個值是為了完整性)。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表 &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
