---
title: MSmerge_partition_groups (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
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
- MSmerge_partition_groups_TSQL
- MSmerge_partition_groups
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_partition_groups system table
ms.assetid: 5d56d780-ee40-4afc-9c2a-d1723d86e430
caps.latest.revision: 13
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: db3ea31b69a96c72bf9c8442b94e891532393d6a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="msmergepartitiongroups-transact-sql"></a>MSmerge_partition_groups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_partition_groups**資料表會針對每個預先計算的資料分割指定的資料庫中儲存一個資料列。 除了列出的資料行之外，還會加入一個資料行，代表參數化資料列篩選器所用的每個函數。 例如，名為資料行**HOST_NAME_FN**會加入至資料表中，如果篩選是使用[HOST_NAME](../../t-sql/functions/host-name-transact-sql.md)函式。 與這個發行者同步處理的每一組唯一函數值，都會各儲存一個資料列代表它。 只要有兩個或兩個以上訂閱者的這些函數完全同值，就會共用這個資料表中的相同資料列，因此也會共用相同的資料分割識別碼。這份資料表儲存在發行集資料庫中。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**partition_id**|**int**|識別提供預先計算的資料分割之唯一識別碼的資料行。|  
|**publication_number**|**smallint**|發行集編號，儲存在**sysmergepublications**。|  
|**maxgen_whenadded**|**bigint**|在將資料列插入這份資料表時，發行者端已知的最高層代 (Generation)。|  
|**using_partition_groups**|**bit**|指出資料分割是否屬於使用預先計算的資料分割之發行集，它可以是下列值之一：<br /><br /> **0** = 發行集不會使用預先計算資料分割。<br /><br /> **1** = 發行集使用預先計算資料分割<br /><br /> 如需詳細資訊，請參閱[使用預先計算的資料分割最佳化參數化篩選效能](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)。|  
|**HOST_NAME_FN**|**nvarchar(128)**|在使用參數化資料列篩選器來產生資料分割時所提供的值。 如需詳細資訊，請參閱 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
