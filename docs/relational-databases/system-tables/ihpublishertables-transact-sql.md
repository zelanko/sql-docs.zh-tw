---
title: IHpublishertables (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHpublishertables
- IHpublishertables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublishertables system table
ms.assetid: 7d16ac39-633a-4fe2-8f22-1d9afc191ee9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d556a80e018a9d3707aa03de7fdefe8c45bcb611
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52802580"
---
# <a name="ihpublishertables-transact-sql"></a>IHpublishertables (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **IHpublishertables**系統資料表代表儲存在發行者端的中繼資料。 此資料表包含從非 SQL Server 發行者發行使用目前散發者的每個來源資料表的一個資料列。 這份資料表儲存在散發資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**table_id**|**int**|識別已發行的資料表。|  
|**publisher_id**|**smallint**|識別非 SQL Server 發行者資料表正在發行。|  
|**name**|**sysname**|已發行之資料表的名稱。|  
|**擁有者**|**sysname**|資料表擁有者。|  
  
## <a name="see-also"></a>另請參閱  
 [異質資料庫複寫](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [複寫資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
