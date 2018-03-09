---
title: "sys.partition_parameters (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- partition_parameters_TSQL
- partition_parameters
- sys.partition_parameters_TSQL
- sys.partition_parameters
dev_langs:
- TSQL
helpviewer_keywords:
- sys.partition_parameters catalog view
ms.assetid: 2012ed9d-3ea3-4c29-9b78-dfa54a392dce
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ea75798552d0521204e063663566b08b36a5797b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="syspartitionparameters-transact-sql"></a>sys.partition_parameters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  針對每個資料分割函數，各包含一個資料列。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**function_id**|**int**|這個參數所屬資料分割函數的識別碼。|  
|**parameter_id**|**int**|參數的識別碼。 它在資料分割函數中是唯一的，以 1 為開頭。|  
|**system_type_id**|**tinyint**|參數系統類型的識別碼。 對應至**system_type_id**資料行**sys.types**目錄檢視。|  
|**max_length**|**smallint**|參數的最大長度 (以位元組為單位)。|  
|**有效位數**|**tinyint**|如果是以數值為基礎，便是參數的有效位數；否則，便是 0。|  
|**小數位數**|**tinyint**|如果是以數值為基礎，便是參數的小數位數；否則，便是 0。|  
|**sys.databases**|**sysname**|如果是以字元為基礎，便是參數的定序名稱；否則，便是 NULL。|  
|**user_type_id**|**int**|類型的識別碼。 在資料庫中，這是唯一的。 對於系統資料類型， **user_type_id** = **system_type_id**。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>請參閱＜  
 [資料分割函數目錄檢視 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/partition-function-catalog-views-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.partition_functions &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-functions-transact-sql.md)   
 [sys.partition_range_values &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-range-values-transact-sql.md)  
  
  
