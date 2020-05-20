---
title: sys.databases external_data_sources （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 1016db6e-9950-4ae2-a004-bd4171e27359
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bbec44831d7025fd53cafe0248eb1f69b79bf14d
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82828162"
---
# <a name="sysexternal_data_sources-transact-sql"></a>sys.external_data_sources (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  針對目前資料庫中、和的每個外部資料源，各包含一個資料列 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSDS](../../includes/sssds-md.md)] [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 。  
  
 針對伺服器上的每個外部資料源，各包含一個資料列 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|data_source_id|**int**|外部資料源的物件識別碼。||  
|name|**sysname**|外部資料源的名稱。||  
|location|**nvarchar(4000)**|連接字串，其中包括通訊協定、IP 位址，以及外部資料源的埠。||  
|type_desc|**nvarchar(255)**|以字串顯示的資料來源類型。|HADOOP、RDBMS、SHARD_MAP_MANAGER、RemoteDataArchiveTypeExtDataSource|  
|類型|**tinyint**|以數字顯示的資料來源類型。|0-HADOOP<br /><br /> 1-RDBMS<br /><br /> 2-SHARD_MAP_MANAGER<br /><br /> 3-RemoteDataArchiveTypeExtDataSource|  
|resource_manager_location|**nvarchar(4000)**|針對類型 HADOOP，這是 Hadoop 資源管理員的 IP 和埠位置。 這是用來在 Hadoop 資料來源上提交作業。<br /><br /> 針對其他類型的外部資料源，則為 Null。||  
|credential_id|**int**|用來連接到外部資料源之資料庫範圍認證的物件識別碼。||  
|database_name|**sysname**|針對類型 RDBMS，為遠端資料庫的名稱。 針對 [類型]，SHARD_MAP_MANAGER，分區對應管理員資料庫的名稱。 針對其他類型的外部資料源，則為 Null。||  
|shard_map_name|**sysname**|針對 [類型 SHARD_MAP_MANAGER]，分區對應的名稱。 針對其他類型的外部資料源，則為 Null。||  
  
## <a name="permissions"></a>權限  
 目錄檢視內中繼資料的可見性會限制在使用者所擁有的安全性實體，或已授與使用者某些權限的安全性實體。  如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [external_file_formats &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-external-file-formats-transact-sql.md)   
 [external_tables &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-external-tables-transact-sql.md)   
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)  
  
  
