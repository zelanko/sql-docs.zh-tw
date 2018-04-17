---
title: MSreplication_objects (TRANSACT-SQL) |Microsoft 文件
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
- MSreplication_objects
- MSreplication_objects_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplication_objects system table
ms.assetid: 08f9710d-976d-448e-bead-ac9835e87bc5
caps.latest.revision: 21
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4b149c9d2a61cdf3529c1c5ae4cce81a1564daed
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="msreplicationobjects-transact-sql"></a>MSreplication_objects (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSreplication_objects**資料表包含每個物件，與在訂閱者資料庫的複寫相關聯的一個資料列。 這份資料表儲存在訂閱資料庫中。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**發行者**|**sysname**|發行者的名稱。|  
|**publisher_db**|**sysname**|發行者資料庫的名稱。|  
|**發行集**|**sysname**|發行集的名稱。|  
|**object_name**|**sysname**|物件的名稱。|  
|**object_type**|**char(2)**|物件類型：<br /><br /> **u** = 資料表。<br /><br /> **t** = 觸發程序。<br /><br /> **p** = 預存程序。|  
|**article**|**sysname**|物件之相關發行項的名稱。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表 &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
