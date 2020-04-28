---
title: sys.databases dm_pdw_nodes_exec_sql_text （Transact-sql） |Microsoft Docs
description: 動態管理檢視會傳回指定之 sql_handle 所識別之 SQL 批次的文字。
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
monikerRange: =azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: fd886217b2fb2caf0fe3f32e88b7bf0215ece1a9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "73145673"
---
# <a name="syspdw_nodes_dm_exec_sql_text-transact-sql"></a>sys.databases pdw_nodes_dm_exec_sql_text （Transact-sql）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

傳回指定之*sql_handle*所識別之 SQL 批次的文字。 這個資料表值函式取代系統函數 **fn_get_sql**。  
   
## <a name="table-returned"></a>傳回的資料表  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**pdw_node_id**|**int**|與節點相關聯的唯一數值識別碼。|
|**dbid**|**smallint**|資料庫的識別碼。<br /><br /> 若為未規劃和備妥的 SQL 語句，則為編譯語句的資料庫識別碼。|  
|**objectid**|**int**|物件的識別碼。<br /><br /> 特定和準備 SQL 陳述式的這個值是 NULL。|  
|**number**|**smallint**|對於已編號的預存程序，這個資料行會傳回預存程序的編號。 如需詳細資訊，請參閱[numbered_procedures &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-numbered-procedures-transact-sql.md)。<br /><br /> 特定和準備 SQL 陳述式的這個值是 NULL。|  
|**encrypted**|**bit**|1： SQL 文字已加密。<br /><br /> 0： SQL 文字未加密。|  
|**text**|**nvarchar(max)**|SQL 查詢的文字。<br /><br /> 加密物件的這個值是 NULL。|  

## <a name="remarks"></a>備註  
[Dm_exec_sql_text](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql?view=sql-server-ver15)適用相同的備註。  
  
## <a name="permissions"></a>權限  
 需要伺服器的**系統管理員（sysadmin** ）伺服器角色或`VIEW SERVER STATE`許可權。  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲動態管理 Views &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  

  ## <a name="next-steps"></a>後續步驟
 如需更多開發秘訣，請參閱 [SQL 資料倉儲開發概觀](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-overview-develop)。