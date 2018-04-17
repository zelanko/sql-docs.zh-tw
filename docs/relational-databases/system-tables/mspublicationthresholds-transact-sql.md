---
title: H (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/04/2017
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
- mspublicationthresholds
- mspublicationthresholds_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpublicationthresholds system table
ms.assetid: 9da3879f-b1f4-4ab4-abd4-a9a8ac395eba
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c34a08a1ea9ff903370369c84ce6c827f08f7283
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="mspublicationthresholds-transact-sql"></a>MSpublicationthresholds (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSpublicationthresholds**資料表用來追蹤發行集，每個受監視的臨界值的其中一個資料列的複寫效能標準。 這份資料表儲存在散發資料庫中。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**publication_id**|**int**|識別設定臨界值的發行集。|  
|**metric_id**|**int**|識別受監視中所定義的複寫效能標準[MSreplmonthresholdmetrics](../../relational-databases/system-tables/msreplmonthresholdmetrics-transact-sql.md)系統資料表。|  
|**value**|**sql_variant**|被監視之標準的臨界值。|  
|**shouldalert**|**bit**|值為**1**指出當標準超過定義的臨界值時，會產生警示。|  
|**isenabled**|**bit**|值為**1**指示，啟用這個複寫效能標準的監視。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
