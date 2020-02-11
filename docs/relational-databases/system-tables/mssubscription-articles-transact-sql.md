---
title: MSsubscription_articles （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsubscription_articles
- MSsubscription_articles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscription_articles system table
ms.assetid: dbc1737f-261e-4017-b9cd-703b9fc4ac78
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8518c787f876152787ee30a20b9f25f936b9fa86
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68139781"
---
# <a name="mssubscription_articles-transact-sql"></a>MSsubscription_articles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSsubscription_articles**表包含佇列訂閱中發行項的相關資訊。 這份資料表只能針對佇列更新和立即更新的複寫類型加以擴展 (佇列更新被當作容錯移轉)。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|服務這個發行項的代理程式識別碼。|  
|**artid**|**int**|**Sysarticles**資料表中的發行項識別碼。|  
|**篇**|**sysname**|**Sysarticles**資料表中的發行項名稱。|  
|**dest_table**|**sysname**|**Sysarticles**資料表中目的地資料表的名稱。|  
|**主人**|**sysname**|訂閱的擁有者。|  
|**cft_table**|**sysname**|這個佇列更新複寫類型之發行項的衝突資料表名稱。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表 &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
