---
title: MSmerge_conflict_&lt;發行&gt;集_&lt;文章&gt; (transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_conflict_publication_article_TSQL
- MSmerge_conflict_publication_article
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_conflict_publication_article system table
ms.assetid: dc4490b4-02d8-4dfc-98f5-0cf8de8e11be
author: stevestein
ms.author: sstein
ms.openlocfilehash: 342b0f51fb4f68945f6ab8c4b511c5299acfba49
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893580"
---
# <a name="msmerge_conflict_ltpublicationgt_ltarticlegt-transact-sql"></a>MSmerge\_衝突\_發行&lt;集文章&gt; (transact-sql)&gt; &lt; \_
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  「 **MSmerge\_衝突\_發行集\_**  」資料表包含衝突的資料列相關資訊, 或針對已復原以達成資料聚合的資料列變更。 發行集中每個複寫的資料表都有衝突資料表，衝突資料表的名稱是附加在發行集和發行項名稱後面。 這些發行項特有的衝突資料表位於記錄衝突所用的資料庫中，通常是發行集資料庫，不過如果是使用非集中式衝突記錄，也可能是訂閱資料庫。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|** _**|**variable**|代表被複寫資料表中的一個資料行。 這個系統資料表包含資料表發行項中每個資料行各一個資料行。|  
|**rowguid**|**uniqueidentifier**|衝突資料列的資料列識別碼。|  
|**ModifiedDate**|**datetime**|發生衝突的時間。|  
|**原始\_資料\_源識別碼**|**uniqueidentifier**|恢復資料列衝突的訂閱，或是遺失衝突的訂閱。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表&#40;transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
