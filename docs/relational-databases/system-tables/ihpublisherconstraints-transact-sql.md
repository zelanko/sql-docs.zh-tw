---
title: "H (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- IHpublisherconstraints
- IHpublisherconstraints_TSQL
dev_langs: TSQL
helpviewer_keywords: IHpublisherconstraints system table
ms.assetid: 537b1e1a-7228-4680-aa27-5ad7072ea01e
caps.latest.revision: "23"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 983f5b6b3d2c572357472b21cb10df129d5cd449
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="ihpublisherconstraints-transact-sql"></a>IHpublisherconstraints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **IHpublisherconstraints**系統資料表包含每個條件約束從非 SQL Server 發行者複寫使用目前散發者的一個資料列。 這份資料表儲存在散發資料庫中。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**publisherconstraint_id**|**int**|識別已發行的條件約束。|  
|**table_id**|**int**|識別從資料表[IHpublishertables](../../relational-databases/system-tables/ihpublishertables-transact-sql.md)所屬的條件約束。|  
|**publisher_id**|**smallint**|識別非 SQL Server 發行者的發行資料行。|  
|**名稱**|**Sysname**|已發行之條件約束的名稱。|  
|**型別**|**nvarchar(255)**|從支援的條件約束類型[IHconstrainttypes](../../relational-databases/system-tables/ihconstrainttypes-transact-sql.md)系統資料表。|  
  
## <a name="see-also"></a>請參閱＜  
 [異質資料庫複寫](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [複寫資料表 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
