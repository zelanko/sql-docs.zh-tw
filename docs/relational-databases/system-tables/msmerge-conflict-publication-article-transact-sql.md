---
title: MSmerge_conflict_publication_article （T-sql）
description: 描述 MSmerge_conflict_publication_article 預存程式，其中包含發生衝突的資料列，或已復原以達成資料聚合之資料列變更的資訊。
ms.custom: seo-lt-2019
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 013e2d1512744d236ac3d8bdd5611e1a2427c2f8
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85736805"
---
# <a name="msmerge_conflict_publication_article-transact-sql"></a>MSmerge_conflict_publication_article （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  **MSmerge_conflict_publication_article**表包含發生衝突的資料列，或已復原以達成資料聚合的資料列變更的資訊。 發行集中每個複寫的資料表都有衝突資料表，衝突資料表的名稱是附加在發行集和發行項名稱後面。 這些發行項特有的衝突資料表位於記錄衝突所用的資料庫中，通常是發行集資料庫，不過如果是使用非集中式衝突記錄，也可能是訂閱資料庫。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**_發行項資料 \_ 行 \_ 名稱_**|**變動**|代表被複寫資料表中的一個資料行。 這個系統資料表包含資料表發行項中每個資料行各一個資料行。|  
|**rowguid**|**uniqueidentifier**|衝突資料列的資料列識別碼。|  
|**ModifiedDate**|**datetime**|發生衝突的時間。|  
|**原始 \_ 資料來源 \_ 識別碼**|**uniqueidentifier**|恢復資料列衝突的訂閱，或是遺失衝突的訂閱。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表 &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
