---
title: sys.dm_pdw_nodes_exec_query_statistics_xml (Transact-sql) |Microsoft Docs
description: 動態管理檢視，會傳回執行中要求的查詢執行計畫。 您可以使用此 DMV 來取得具有暫時性統計資料的執行程式表 XML。
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
ms.openlocfilehash: 540a5632997c025a98e259e23f87780134649b75
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97482549"
---
# <a name="dm_pdw_nodes_exec_query_statistics_xml-transact-sql"></a>dm_pdw_nodes_exec_query_statistics_xml (Transact-sql) 
[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

傳回進行中要求的查詢執行計畫。 您可以使用此 DMV 來取得具有暫時性統計資料的執行程式表 XML。

## <a name="table-returned"></a>傳回的資料表

|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|
|node_id|**int**|與節點相關聯的唯一數值識別碼。|
|session_id|**smallint**|工作階段的識別碼。 不可為 Null。|
|request_id|**int**|要求的識別碼。 不可為 Null。|
|sql_handle|**varbinary(64)**|這是可唯一識別查詢所屬批次或預存程式的 token。 可為 Null。|
|plan_handle|**varbinary(64)**|這是一個 token，可唯一識別目前正在執行之批次的查詢執行計畫。 可為 Null。|
|query_plan|**xml**|包含查詢執行計畫的執行時間執行程式表表示，此計畫是以包含部分統計資料 *plan_handle* 指定的。 顯示計畫是 XML 格式。 每個包含諸如特定 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式、預存程序呼叫和使用者自訂函數呼叫的批次，都會產生一份計畫。 可為 Null。|

## <a name="remarks"></a>備註
[Sys.dm_exec_query_statistics_xml](./sys-dm-exec-query-statistics-xml-transact-sql.md?view=sql-server-ver15)中的相同備註也適用。   

## <a name="permissions"></a>權限  
 需要伺服器的 `VIEW SERVER STATE` 權限。  

## <a name="see-also"></a>另請參閱  
 [Azure Synapse Analytics 和平行處理資料倉儲動態管理檢視 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  

 ## <a name="next-steps"></a>後續步驟
 如需更多開發秘訣，請參閱 [Azure Synapse Analytics 開發總覽](/azure/sql-data-warehouse/sql-data-warehouse-overview-develop)。