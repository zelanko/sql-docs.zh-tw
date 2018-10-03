---
title: MSsubscription_articles (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
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
manager: craigg
ms.openlocfilehash: 767df03bda9a11ce629244b15e83b7dc676894a9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47691758"
---
# <a name="mssubscriptionarticles-transact-sql"></a>MSsubscription_articles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSsubscription_articles**資料表包含佇列式訂閱中的發行項資訊。 這份資料表只能針對佇列更新和立即更新的複寫類型加以擴展 (佇列更新被當作容錯移轉)。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|服務這個發行項的代理程式識別碼。|  
|**artid&lt**|**int**|發行項識別碼**sysarticles**資料表。|  
|**article**|**sysname**|從發行項名稱**sysarticles**資料表。|  
|**dest_table**|**sysname**|目的地資料表名稱**sysarticles**資料表。|  
|**擁有者**|**sysname**|訂閱的擁有者。|  
|**cft_table**|**sysname**|這個佇列更新複寫類型之發行項的衝突資料表名稱。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
