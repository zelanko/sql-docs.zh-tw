---
description: MSpublicationthresholds (Transact-SQL)
title: MSpublicationthresholds (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- mspublicationthresholds
- mspublicationthresholds_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpublicationthresholds system table
ms.assetid: 9da3879f-b1f4-4ab4-abd4-a9a8ac395eba
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8f43705f8fec92e39e55a4fa4f62cf24aa9f25be
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540297"
---
# <a name="mspublicationthresholds-transact-sql"></a>MSpublicationthresholds (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSpublicationthresholds**資料表是用來追蹤發行集的複寫效能標準，每個監視的臨界值都有一個資料列。 這份資料表儲存在散發資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**publication_id**|**int**|識別設定臨界值的發行集。|  
|**metric_id**|**int**|識別要監視的複寫效能度量，如 [MSreplmonthresholdmetrics](../../relational-databases/system-tables/msreplmonthresholdmetrics-transact-sql.md) 系統資料表中所定義。|  
|**value**|**sql_variant**|被監視之標準的臨界值。|  
|**shouldalert**|**bit**|值為 **1** 時，表示當度量超出定義的閾值時，應產生警示。|  
|**isenabled**|**bit**|值為 **1** 表示已針對此複寫效能標準啟用監視。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表 &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
