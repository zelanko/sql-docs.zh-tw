---
title: sys.dm_pdw_nodes_exec_text_query_plan (Transact-sql) |Microsoft Docs
description: 動態管理檢視，可針對 TSQL 批次或批次內的特定語句，以文字格式傳回顯示計畫。
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
ms.openlocfilehash: b2926817399e0e7604279d25fe46f0a944117a49
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97440783"
---
# <a name="sysdm_pdw_nodes_exec_text_query_plan--transact-sql"></a>sys.dm_pdw_nodes_exec_text_query_plan (Transact-sql) 
[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

針對 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批次或批次內的特定陳述式，以文字格式傳回顯示計畫。

## <a name="table-returned"></a>傳回的資料表  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**pdw_node_ID**|**int**|與節點相關聯的唯一數值識別碼。|
|**dbid**|**smallint**|當編譯對應於這個計畫的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式時，作用中內容資料庫的識別碼。 對於隨選和準備的 SQL 陳述式而言，則為編譯陳述式的資料庫識別碼。<br /><br /> 資料行可為 Null。|  
|**objectid**|**int**|這個查詢計畫的物件識別碼 (如預存程序或使用者自訂函數)。 若為特定和準備批次，這個資料行是 **Null**。<br /><br /> 資料行可為 Null。|  
|**number**|**smallint**|編號預存程序整數。 若為特定和準備批次，這個資料行是 **Null**。<br /><br /> 資料行可為 Null。| 
|**加密**|**bit**|指出對應的預存程序是否加密。<br /><br /> 0 = 未加密<br /><br /> 1 = 加密<br /><br /> 資料行不可為 Null。|  
|**query_plan**|**nvarchar(max)**|包含以 *plan_handle* 指定之查詢執行計畫的編譯階段顯示計畫標記法。 顯示計畫是文字格式。 每個包含諸如特定 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式、預存程序呼叫和使用者自訂函數呼叫的批次，都會產生一份計畫。<br /><br /> 資料行可為 Null。|  

## <a name="remarks"></a>備註  
[Sys.dm_exec_text_query_plan](./sys-dm-exec-text-query-plan-transact-sql.md?view=sql-server-ver15)中的相同備註也適用。  

## <a name="permissions"></a>權限  
 需要伺服器的 **系統管理員（sysadmin** ）伺服器角色或 `VIEW SERVER STATE` 許可權。  
  
## <a name="see-also"></a>另請參閱  
 [Azure Synapse Analytics 和平行處理資料倉儲動態管理檢視 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  

  ## <a name="next-steps"></a>後續步驟
 如需更多開發秘訣，請參閱 [Azure Synapse Analytics 開發總覽](/azure/sql-data-warehouse/sql-data-warehouse-overview-develop)。