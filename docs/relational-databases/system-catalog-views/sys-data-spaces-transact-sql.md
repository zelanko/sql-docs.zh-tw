---
title: sys.data_spaces (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- data_spaces
- sys.data_spaces_TSQL
- sys.data_spaces
- data_spaces_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.data_spaces catalog view
ms.assetid: f39d55fe-2c0f-472d-a77f-cebc6fea95b5
caps.latest.revision: 34
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9e41ed120be84ed194ee9bee5f7f87166d21c532
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43080339"
---
# <a name="sysdataspaces-transact-sql"></a>sys.data_spaces (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  針對每個資料空間，各包含一個資料列。 這可以是檔案群組、分割區配置或 FILESTREAM 資料檔案群組。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|NAME|**sysname**|資料空間的名稱，它在資料庫中是唯一的。|  
|data_space_id|**int**|資料空間識別碼，它在資料庫中是唯一的。|  
|型別|**char(2)**|資料空間類型：<br /><br /> FG = 檔案群組<br /><br /> FD = FILESTREAM 資料檔案群組<br /><br /> FX = 記憶體最佳化的資料表檔案群組<br /><br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> PS = 分割區配置|  
|type_desc|**nvarchar(60)**|資料空間類型的描述：<br /><br /> FILESTREAM_DATA_FILEGROUP<br /><br /> MEMORY_OPTIMIZED_DATA_FILEGROUP<br /><br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> PARTITION_SCHEME<br /><br /> ROWS_FILEGROUP|  
|is_default|**bit**|1 = 這是預設的資料空間。 如果 CREATE TABLE 或 CREATE INDEX 陳述式沒有指定檔案群組或分割區區配置，則會使用預設資料空間。<br /><br /> 0 = 這不是預設的資料空間。|  
|is_system|**bit**|**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 1 = 將資料空間用於全文檢索索引片段。<br /><br /> 0 = 不將資料空間用於全文檢索索引片段。|  
  
## <a name="permissions"></a>Permissions  
 需要 public 角色中的成員資格。 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [資料空間&#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/data-spaces-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.destination_data_spaces &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-destination-data-spaces-transact-sql.md)   
 [sys.filegroups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [sys.partition_schemes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-schemes-transact-sql.md)   
 [查詢 SQL Server 系統目錄常見問題集](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
