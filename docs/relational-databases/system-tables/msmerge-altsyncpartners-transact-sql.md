---
description: MSmerge_altsyncpartners (Transact-SQL)
title: MSmerge_altsyncpartners (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_altsyncpartners_TSQL
- MSmerge_altsyncpartners
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_altsyncpartners system table
ms.assetid: da51b0f8-5ad0-4aeb-96ed-2b3672a2a6e2
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ccec6fa369580fd68af0089c7e581ef1e915e868
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545650"
---
# <a name="msmerge_altsyncpartners-transact-sql"></a>MSmerge_altsyncpartners (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSmerge_altsyncpartners**資料表會追蹤目前的同步處理夥伴對於發行者的關聯。 這份資料表儲存在發行集和訂閱資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**subid**|**uniqueidentifier**|原始發行者的識別碼。|  
|**alternate_subid**|**uniqueidentifier**|替代同步處理夥伴之訂閱者的識別碼。|  
|**description**|**nvarchar(255)**|替代同步處理夥伴的描述。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表 &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
