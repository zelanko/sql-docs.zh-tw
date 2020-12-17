---
title: sys.dm_pdw_nodes_exec_sql_text (Transact-sql) |Microsoft Docs
description: 動態管理檢視，會傳回指定 sql_handle 所識別之 SQL 批次的文字。
ms.custom: ''
ms.date: 10/14/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: ''
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: =azure-sqldw-latest
ms.openlocfilehash: b4e4c686411d40a2c161c670821e6566460db4a4
ms.sourcegitcommit: 370cab80fba17c15fb0bceed9f80cb099017e000
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/17/2020
ms.locfileid: "97644061"
---
# <a name="syspdw_nodes_dm_exec_sql_text-transact-sql"></a>sys.pdw_nodes_dm_exec_sql_text (Transact-sql) 
[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

傳回指定 *sql_handle* 所識別之 SQL 批次的文字。 這個資料表值函式取代系統函數 **fn_get_sql**。  
   
## <a name="table-returned"></a>傳回的資料表  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**pdw_node_id**|**int**|與節點相關聯的唯一數值識別碼。|
|**dbid**|**smallint**|資料庫的識別碼。<br /><br /> 若為未規劃和已備妥的 SQL 語句，則為編譯語句的資料庫識別碼。|  
|**objectid**|**int**|物件的識別碼。<br /><br /> 特定和準備 SQL 陳述式的這個值是 NULL。|  
|**number**|**smallint**|對於已編號的預存程序，這個資料行會傳回預存程序的編號。 如需詳細資訊，請參閱 [sys.numbered_procedures &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-numbered-procedures-transact-sql.md)。<br /><br /> 特定和準備 SQL 陳述式的這個值是 NULL。|  
|**加密**|**bit**|1： SQL 文字已加密。<br /><br /> 0： SQL 文字未加密。|  
|**text**|**nvarchar(max)**|SQL 查詢的文字。<br /><br /> 加密物件的這個值是 NULL。|  

## <a name="remarks"></a>備註  
[Sys.dm_exec_sql_text](./sys-dm-exec-sql-text-transact-sql.md)中的相同備註也適用。  
  
## <a name="permissions"></a>權限  
 需要伺服器的 **系統管理員（sysadmin** ）伺服器角色或 `VIEW SERVER STATE` 許可權。  
  
## <a name="see-also"></a>另請參閱  
 [Azure Synapse Analytics 和平行處理資料倉儲動態管理檢視 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  

  ## <a name="next-steps"></a>後續步驟
 如需更多開發秘訣，請參閱 [Azure Synapse Analytics 開發總覽](/azure/sql-data-warehouse/sql-data-warehouse-overview-develop)。