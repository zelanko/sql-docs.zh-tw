---
title: trace_xe_action_map (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- trace_xe_action_map_TSQL
- trace_xe_action_map
dev_langs:
- TSQL
helpviewer_keywords:
- extended events [SQL Server], tables
- trace_xe_action_map
ms.assetid: 208a1413-ce7f-4521-b765-d74723627302
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7308df1dafe80d4c4b342c6b5797db6354f98416
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47827176"
---
# <a name="extended-events-tables---tracexeactionmap"></a>擴充事件資料表 - trace_xe_action_map
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  針對對應到 SQL 追蹤資料行識別碼的每個擴充事件動作包含一個資料列。 這份資料表儲存在 master 資料庫的 sys 結構描述中。  
  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|trace_column_id|**smallint**|對應之 SQL 追蹤資料行的識別碼。|  
|package_name|**nvarchar(60)**|對應動作所在之擴充事件封裝的名稱。|  
|xe_action_name|**nvarchar(60)**|對應至 SQL 追蹤資料行之擴充事件動作的名稱。|  
  
## <a name="remarks"></a>備註  
 您可以使用下列查詢來識別相當於 SQL 追蹤資料行的擴充事件動作：  
  
```  
SELECT tc.name AS trace_column, am.package_name, am.xe_action_name  
FROM sys.trace_columns AS tc  
INNER JOIN sys.trace_xe_action_map AS am  
   ON tc.trace_column_id = am.trace_column_id  
```  
  
 資料表中不包含未對應到動作的 SQL 追蹤資料行。  
  
## <a name="see-also"></a>另請參閱  
 [trace_xe_event_map &#40;Transact-SQL&#41;](../../relational-databases/system-tables/extended-events-tables-trace-xe-event-map.md)  
  
  
