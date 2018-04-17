---
title: MSmerge_conflict_&lt;發行集&gt;_&lt;文章&gt;(TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/16/2017
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
- MSmerge_conflict_publication_article_TSQL
- MSmerge_conflict_publication_article
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_conflict_publication_article system table
ms.assetid: dc4490b4-02d8-4dfc-98f5-0cf8de8e11be
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4e82334105648183a9a5ad4d695f278949e51c07
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="msmergeconflictltpublicationgtltarticlegt-transact-sql"></a>MSmerge_conflict_&lt;發行集&gt;_&lt;文章&gt;(TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_conflict_*發行集*_ * 文章*** 資料表包含衝突資料列的或已復原，以達到資料聚合目的的資料列變更的資訊。 發行集中每個複寫的資料表都有衝突資料表，衝突資料表的名稱是附加在發行集和發行項名稱後面。 這些發行項特有的衝突資料表位於記錄衝突所用的資料庫中，通常是發行集資料庫，不過如果是使用非集中式衝突記錄，也可能是訂閱資料庫。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|***article_column_name***|**variable**|代表被複寫資料表中的一個資料行。 這個系統資料表包含資料表發行項中每個資料行各一個資料行。|  
|**rowguid**|**uniqueidentifier**|衝突資料列的資料列識別碼。|  
|**ModifiedDate**|**datetime**|發生衝突的時間。|  
|**origin_datasource_id**|**uniqueidentifier**|恢復資料列衝突的訂閱，或是遺失衝突的訂閱。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
