---
title: sys.dm_repl_schemas (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_repl_schemas_TSQL
- dm_repl_schemas
- sys.dm_repl_schemas_TSQL
- sys.dm_repl_schemas
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_repl_schemas dynamic management function
ms.assetid: 6f5fefff-8492-4360-bd5b-a97287367914
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3f1ae6561bc96f5d4dff4d21a6057a4c1b9816c4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmreplschemas-transact-sql"></a>sys.dm_repl_schemas (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回有關複寫發行之資料表資料行的資訊。  
  
 
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**artcache_schema_address**|**varbinary(8)**|已發行之資料表發行項的快取結構描述結構的記憶體中位址。|  
|**tabid**|**bigint**|複寫資料表的識別碼。|  
|**indexid**|**smallint**|已發行資料表之叢集索引的識別碼。|  
|**idSch**|**bigint**|資料表結構描述的識別碼。|  
|**tabschema**|**nvarchar(510)**|資料表結構描述的名稱。|  
|**ccTabschema**|**smallint**|資料表結構描述的字元長度。|  
|**tabname**|**nvarchar(510)**|已發行資料表的名稱。|  
|**ccTabname**|**smallint**|已發行資料表名稱的字元長度。|  
|**rowsetid_delete**|**bigint**|已刪除資料列的識別碼。|  
|**rowsetid_insert**|**bigint**|已插入資料列的識別碼。|  
|**num_pk_cols**|**int**|主索引鍵資料行的數目。|  
|**pcitee**|**binary(8000)**|用來評估計算資料行之查詢運算式結構的指標。|  
|**re_numtextcols**|**int**|已複寫資料表中的二進位大型物件資料行數目。|  
|**re_schema_lsn_begin**|**binary(8000)**|結構描述版本記錄的開始記錄序號 (LSN)。|  
|**re_schema_lsn_end**|**binary(8000)**|結構描述版本記錄的結束 LSN。|  
|**re_numcols**|**int**|已發行的資料行數目。|  
|**re_colid**|**int**|在發行者端的資料行識別碼。|  
|**re_awcName**|**nvarchar(510)**|已發行資料行的名稱。|  
|**re_ccName**|**smallint**|資料行名稱的字元數目。|  
|**re_pk**|**tinyint**|已發行資料行是否為主索引鍵的一部分。|  
|**re_unique**|**tinyint**|已發行資料行是否為唯一索引的一部分。|  
|**re_maxlen**|**smallint**|已發行資料行的最大長度。|  
|**re_prec**|**tinyint**|已發行資料行的有效位數。|  
|**re_scale**|**tinyint**|已發行資料行的小數位數。|  
|**re_collatid**|**bigint**|已發行資料行的定序識別碼。|  
|**re_xvtype**|**smallint**|已發行資料行的類型。|  
|**re_offset**|**smallint**|已發行資料行的位移。|  
|**re_bitpos**|**tinyint**|已發行資料行的位元位置 (以位元組向量為單位)。|  
|**re_fNullable**|**tinyint**|指定已發行資料行是否支援 NULL 值。|  
|**re_fAnsiTrim**|**tinyint**|指定 ANSI 修剪是否用於已發行資料行。|  
|**re_computed**|**smallint**|指定已發行資料行是否為計算資料行。|  
|**se_rowsetid**|**bigint**|資料列集的識別碼。|  
|**se_schema_lsn_begin**|**binary(8000)**|結構描述版本記錄的開始 LSN。|  
|**se_schema_lsn_end**|**binary(8000)**|結構描述版本記錄的結束 LSN。|  
|**se_numcols**|**int**|資料行數目。|  
|**se_colid**|**int**|在訂閱者端的資料行識別碼。|  
|**se_maxlen**|**smallint**|資料行的最大長度。|  
|**se_prec**|**tinyint**|資料行的有效位數。|  
|**se_scale**|**tinyint**|資料行的小數位數。|  
|**se_collatid**|**bigint**|資料行的定序識別碼。|  
|**se_xvtype**|**smallint**|資料行的類型。|  
|**se_offset**|**smallint**|資料行的位移。|  
|**se_bitpos**|**tinyint**|資料行的位元位置 (以位元組向量為單位)。|  
|**se_fNullable**|**tinyint**|指定資料行是否支援 NULL 值。|  
|**se_fAnsiTrim**|**tinyint**|指定 ANSI 修剪是否用於資料行。|  
|**se_computed**|**smallint**|指定資料行是否為計算資料行。|  
|**se_nullBitInLeafRows**|**int**|指定資料行值是否為 NULL。|  
  
## <a name="permissions"></a>Permissions  
 需要 VIEW DATABASE STATE 權限在發行集資料庫上的呼叫**dm_repl_schemas**。  
  
## <a name="remarks"></a>備註  
 只對目前載入複寫發行項快取中的複寫資料庫物件傳回這項資訊。  
  
## <a name="see-also"></a>另請參閱  
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [複寫相關的動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/replication-related-dynamic-management-views-transact-sql.md)  
  
  

