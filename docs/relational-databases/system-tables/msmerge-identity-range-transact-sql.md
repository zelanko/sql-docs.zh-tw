---
title: MSmerge_identity_range (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
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
- MSmerge_identity_range_TSQL
- MSmerge_identity_range
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_identity_range system table
ms.assetid: 493a2028-88a0-4e83-ad89-ae5661d9f477
caps.latest.revision: 21
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bbd06dae4c34b2b5c77b81db64f9d12408539b01
ms.sourcegitcommit: a431ca21eac82117492d7b84c398ddb3fced53cc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/17/2018
ms.locfileid: "39101226"
---
# <a name="msmergeidentityrange-transact-sql"></a>MSmerge_identity_range (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_identity_range**資料表用來追蹤指派給識別欄位以訂閱發行集的數值範圍而複寫會自動管理這些範圍指派。 這份資料表儲存在發行集和訂閱資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**subid**|**uniqueidentifier**|給定訂閱的唯一識別碼。|  
|**artid&lt**|**uniqueidentifier**|給定發行項的唯一識別碼。|  
|**: range_begin**|**numeric(38)**|在目前範圍開頭的識別值。|  
|**range_end**|**numeric(38)**|在目前範圍結尾的識別值。|  
|**next_range_begin**|**numeric(38)**|在下一個要指派之範圍開頭的識別值。|  
|**next_range_end**|**numeric(38)**|在下一個要指派之範圍結尾的識別值。|  
|**is_pub_range**|**bit**|值為**1**如果識別範圍指派給發行集。|  
|**max_used**|**numeric(38)**|所能指派的最大識別值。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
