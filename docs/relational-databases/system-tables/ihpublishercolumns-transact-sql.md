---
title: IHpublishercolumns (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
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
- IHpublishercolumns
- IHpublishercolumns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublishercolumns system table
ms.assetid: a5347750-224c-40d9-ae12-57e7213b7db9
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1032578837699182d4c1ba73a118d03ece01b5f6
ms.sourcegitcommit: a431ca21eac82117492d7b84c398ddb3fced53cc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/17/2018
ms.locfileid: "39103867"
---
# <a name="ihpublishercolumns-transact-sql"></a>IHpublishercolumns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **IHpublishercolumns**系統資料表代表儲存在發行者端的中繼資料。 此資料表包含每個資料行從非 SQL Server 發行者複寫使用目前散發者的一個資料列。 資料型別中的資訊**IHpublishercolumns**特有發行資料的非 SQL Server 資料庫管理系統 (DBMS)。 這份資料表儲存在散發資料庫中。  
  
## <a name="definition"></a>定義  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**publishercolumn_id**|**int**|識別已發行的資料行。|  
|**table_id**|**int**|識別來源資料表，從[IHpublishertables](../../relational-databases/system-tables/ihpublishertables-transact-sql.md)所屬資料行。|  
|**publisher_id**|**smallint**|識別非 SQL Server 發行者的發行資料行。|  
|**name**|**sysname**|已發行的資料行名稱。|  
|**column_ordinal**|**int**|依序識別欄位。|  
|**type**|**varchar(255)**|發行者之來源資料行的資料行資料類型。|  
|**長度**|**bigint**|發行者的來源資料行長度。|  
|**prec**|**int**|發行者來源資料行的有效位數。|  
|**scale**|**int**|發行者來源資料行的小數位數。|  
|**isnullable**|**bit**|指出資料行是否接受 NULL 值，其中**1**表示接受 NULL 值。|  
|**iscaptured**|**bit**|指出資料行是否有觸發程序存在 (即使發行項中沒有發行該資料行，也可能存在)。 值為**1**表示資料行有觸發程序。|  
  
## <a name="see-also"></a>另請參閱  
 [異質資料庫複寫](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [複寫資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視&#40;Transact SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sysarticlecolumns&#40;系統檢視&#41; &#40;TRANSACT-SQL&#41;](../../relational-databases/system-views/sysarticlecolumns-system-view-transact-sql.md)   
 [sysarticlecolumns &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-tables/sysarticlecolumns-transact-sql.md)  
  
  
