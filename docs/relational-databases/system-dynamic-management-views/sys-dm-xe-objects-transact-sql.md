---
title: sys.dm_xe_objects (TRANSACT-SQL) |Microsoft 文件
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
- dm_xe_objects
- sys.dm_xe_objects
- sys.dm_xe_objects_TSQL
- dm_xe_objects_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xe_objects dynamic management view
- extended events [SQL Server], views
ms.assetid: 5d944b99-b097-491b-8cbd-b0e42b459ec0
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f9f317555f992261eb76d65dae4e7d0e91163f71
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmxeobjects-transact-sql"></a>sys.dm_xe_objects (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對事件封裝所公開的每個物件，各傳回一個資料列。 物件可以是下列其中一項：  
  
-   事件。 事件會指示執行路徑中所要的點。 所有的事件都包含所要之點的相關資訊。  
  
-   動作。 當事件引發時，會以同步方式執行動作。 動作可以將執行階段資料附加至事件。  
  
-   目標。 目標會耗用事件 (在引發事件的執行緒上同步處理，或是在系統提供的執行緒上非同步處理)。  
  
-   述詞。 述詞來源會從事件來源中擷取值，以供比較作業使用。 述詞比較作業會比較特定的資料類型，並傳回布林值。  
  
-   類型。 類型會封裝位元組集合的長度和特性，以便能夠解譯資料。  

 |資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|name|**nvarchar(60)**|物件的名稱。 名稱是唯一在封裝中的特定物件類型。 不可為 Null。|  
|object_type|**nvarchar(60)**|物件的型別。 object_type 是下列其中一項：<br /><br /> event<br /><br /> action<br /><br /> 目標<br /><br /> pred_source<br /><br /> pred_compare<br /><br /> 型別<br /><br /> 不可為 Null。|  
|package_guid|**uniqueidentifier**|公開此動作之封裝的 GUID。 這與 sys.dm_xe_packages.package_id 之間是多對一的關聯性。 不可為 Null。|  
|description|**nvarchar(256)**|動作的描述。 描述是由封裝作者所設定。 不可為 Null。|  
|capabilities|**int**|描述此物件之功能的點陣圖。 可為 Null。|  
|capabilities_desc|**nvarchar(256)**|列出此物件的所有功能。 可為 Null。<br /><br /> **套用到所有物件類型的功能**<br /><br /> —<br />                                **私用**。 唯一供內部使用的物件，而且無法透過 CREATE/ALTER EVENT SESSION DDL 加以存取。 除了在內部使用的少量物件以外，稽核事件和目標也屬於這個類別目錄。<br /><br /> ===============<br /><br /> **事件功能**<br /><br /> —<br />                                **No_block**。 事件位於任何原因都無法封鎖的關鍵程式碼路徑中。 具有此功能的事件可能無法加入指定 NO_EVENT_LOSS 的任何事件工作階段。<br /><br /> ===============<br /><br /> **套用到所有物件類型的功能**<br /><br /> —<br />                                **Process_whole_buffers**。 目標一次會耗用事件緩衝區，而不是逐一事件。<br /><br /> —<br />                        **單一**。 只有一個目標執行個體可以存在處理序中。 雖然多個事件工作階段可以參考相同的單一目標，但是其實只有一個執行個體，而且該執行個體只會看到每一個唯一事件一次。 如果要將目標加入至全部收集相同事件的多個工作階段，這就會非常重要。<br /><br /> —<br />                                **Synchronous**： 將控制權送回呼叫的程式碼行之前，會在產生事件的執行緒上執行目標。|  
|type_name|**nvarchar(60)**|pred_source 和 pred_compare 物件的名稱。 可為 Null。|  
|type_package_guid|**uniqueidentifier**|公開此物件操作所在之類型的封裝 GUID。 可為 Null。|  
|type_size|**int**|資料類型的大小 (以位元組為單位)。 只適用於有效的物件類型。 可為 Null。|  
  
## <a name="permissions"></a>Permissions  
 需要伺服器的 VIEW SERVER STATE 權限。  
  
### <a name="relationship-cardinalities"></a>關聯性基數  
  
|來源|若要|關聯性|  
|----------|--------|------------------|  
|sys.dm_xe_objects.package_guid|sys.dm_xe_packages.guid|多對一|  
  
## <a name="see-also"></a>另請參閱  
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

