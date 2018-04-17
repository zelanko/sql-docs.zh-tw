---
title: IHpublishercolumnindexes (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
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
- IHpublishercolumnindexes
- IHpublishercolumnindexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublishercolumnindexes system table
ms.assetid: 95b95a1d-b502-4838-825f-82a456487e25
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fda5b9cc5d5f1e86a780463831e358c55248cef6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="ihpublishercolumnindexes-transact-sql"></a>IHpublishercolumnindexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **IHpublishercolumnindexes**系統資料表對應中的非 SQL Server 發行集的資料行[IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md)系統資料表中的索引[IHpublisherindexes](../../relational-databases/system-tables/ihpublisherindexes-transact-sql.md)系統資料表。 這份資料表儲存在散發資料庫中。  
  
## <a name="definition"></a>定義  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**publishercolumn_id**|**int**|識別資料行從[IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md)具有相關聯的索引。|  
|**publisherindex_id**|**int**|識別從索引[IHpublisherindexes](../../relational-databases/system-tables/ihpublisherindexes-transact-sql.md)資料表資料行相關聯。|  
|**indid**|**int**|指出該資料行在已發行資料表中的位置。|  
  
## <a name="see-also"></a>另請參閱  
 [異質資料庫複寫](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [複寫資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
