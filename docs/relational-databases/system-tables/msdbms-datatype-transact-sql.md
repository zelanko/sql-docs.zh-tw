---
title: M (TRANSACT-SQL) |Microsoft 文件
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
- MSdbms_datatype
- MSdbms_datatype_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdbms_datatype system table
ms.assetid: 606168cc-79a8-442f-ab43-936f8f884d72
caps.latest.revision: 24
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 5927d0c839793e58b2bc6422fa9f3646b0538699
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33004675"
---
# <a name="msdbmsdatatype-transact-sql"></a>MSdbms_datatype (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSdbms_datatype**資料表包含每個支援的資料庫管理系統 (DBMS) 在異質資料庫複寫中作為發行者或訂閱者使用的原生資料類型的完整清單。 這份資料表儲存在**msdb**資料庫。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**msdbms_datatype**|**int**|識別每個唯一資料類型。|  
|**msdbms**|**int**|識別類型所屬的 DBMS。|  
|**type**|**sysname**|資料類型名稱 (原生)。|  
|**createparams**|**int**|用來描述每個資料類型所適用之長度、有效位數和小數位數組合的點陣圖，其中包括：<br /><br /> **0x1** = 有效位數。<br /><br /> **0x2** = 小數位數。<br /><br /> **0x4** = 長度。|  
  
## <a name="remarks"></a>備註  
 此資料表包含 SQL Server 資料類型的項目，因為 SQL Server 執行個體可以訂閱非 SQL Server 資料庫中，而且發行到非 SQL Server 訂閱者。  
  
## <a name="see-also"></a>另請參閱  
 [異質資料庫複寫](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [指定 「 Oracle 發行者 」 的資料類型對應](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [複寫資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
