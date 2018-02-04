---
title: sys.dm_xe_packages (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_xe_packages_TSQL
- sys.dm_xe_packages_TSQL
- dm_xe_packages
- sys.dm_xe_packages
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xe_packages dynamic management view
- extended events [SQL Server], views
ms.assetid: 2e5ecbe9-3ea8-45e6-a161-e31671a03e1d
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d33b1703f517fbedb746d1a0185e960764603ff5
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmxepackages-transact-sql"></a>sys.dm_xe_packages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  列出已向擴充的事件引擎註冊的所有封裝。  
  
 
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|name|**nvarchar(60)**|封裝的名稱。 描述會從封裝本身公開。 不可為 Null。|  
|guid|**uniqueidentifier**|識別此封裝的 GUID。 不可為 Null。|  
|description|**nvarchar(256)**|封裝的描述。 descriptionis 由封裝作者所設定，並不是可為 null。|  
|capabilities|**int**|描述這個封裝之功能的點陣圖。 可為 Null。|  
|capabilities_desc|**nvarchar(256)**|此封裝所有可能之功能的清單。 可為 Null。|  
|module_guid|**uniqueidentifier**|公開此封裝之模組的 GUID。 不可為 Null。|  
|module_address|**varbinary(8)**|載入包含封裝之模組的基底位址。 單一模組可能會公開數個封裝。 不可為 Null。|  
  
## <a name="permissions"></a>Permissions  
 需要伺服器的 VIEW SERVER STATE 權限。  
  
## <a name="remarks"></a>備註  
 向擴充的事件引擎註冊的封裝會公開事件、事件引發時可以採取的動作，以及同步和非同步處理事件資料的目標。  
  
 這些封裝可以動態地載入處理序位址空間。 當載入封裝時，它會向擴充的事件引擎註冊它所公開的所有物件。  
  
## <a name="relationship-cardinalities"></a>關聯性基數  
  
||||  
|-|-|-|  
|來源|若要|關聯性|  
|sys.dm_xe_packages.module_address|sys.dm_os_loaded_modules.base_address|多對一|  
  
## <a name="see-also"></a>另請參閱  
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

