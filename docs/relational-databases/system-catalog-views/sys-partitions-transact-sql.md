---
title: sys.databases （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- partitions
- partitions_TSQL
- sys.partitions_TSQL
- sys.partitions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.partitions catalog view
ms.assetid: 1c19e1b1-c925-4dad-a652-581692f4ab5e
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 39ae65e980d8f35f3a59d2f1d17481fed4d2a596
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82831511"
---
# <a name="syspartitions-transact-sql"></a>sys.partitions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  針對資料庫中所有資料表和大部分類型索引的每個資料分割，都各包含一個資料列。 這個檢視表中不包含特殊索引類型，例如全文檢索、空間和 XML。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的所有資料表和索引都至少包含一個資料分割，不論它們是否進行明確的資料分割都一樣。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|partition_id|**bigint**|指出資料分割識別碼。 在資料庫中，這是唯一的。|  
|object_id|**int**|指出這個資料分割所屬物件的識別碼。 每份資料表或檢視表至少都是由一個資料分割組成。|  
|index_id|**int**|指出這個資料分割所屬物件內的索引識別碼。<br /><br /> 0 = 堆積<br />1 = 叢集索引<br />2 或以上 = 非叢集索引|  
|partition_number|**int**|這是在擁有索引或堆積內，以 1 為底的資料分割編號。 如果是非資料分割的資料表和索引，這個資料行的值便是 1。|  
|hobt_id|**bigint**|表示資料堆積或 B 型樹狀目錄（HoBT）的識別碼，其中包含此分割區的資料列。|  
|rows|**bigint**|指出這個資料分割中的近似資料列數。|  
|filestream_filegroup_id|**smallint**|**適用對象**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 及更新版本。<br /><br /> 指出儲存在這個資料分割上之 FILESTREAM 檔案群組的識別碼。|  
|data_compression|**tinyint**|表示每個資料分割的壓縮狀態：<br /><br /> 0 = NONE <br />1 = ROW <br />2 = PAGE <br />3 = 資料行存放區：**適用于**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 及更新版本<br />4 = COLUMNSTORE_ARCHIVE：**適用于**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 和更新版本<br /><br /> **注意：** 所有版本的都將壓縮全文檢索索引 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。|  
|data_compression_desc|**nvarchar(60)**|表示每個資料分割的壓縮狀態。 資料列存放區資料表的可能值為 NONE、ROW 和 PAGE。 資料行存放區資料表的可能值為 COLUMNSTORE 和 COLUMNSTORE_ARCHIVE。|  
  
## <a name="permissions"></a>權限  
 需要 **public** 角色的成員資格。  如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的物件目錄檢視](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [&#40;Transact-sql&#41;的目錄檢視](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查詢 SQL Server 系統目錄 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
