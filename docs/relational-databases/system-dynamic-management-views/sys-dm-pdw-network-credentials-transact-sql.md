---
title: sys.databases dm_pdw_network_credentials （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d4fee3ad-6285-4ea5-8513-5e6eb617abb0
author: stevestein
ms.author: sstein
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: b75eb53da9961025e3310f27e4a12608dd4fda78
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67899353"
---
# <a name="sysdm_pdw_network_credentials-transact-sql"></a>sys.databases dm_pdw_network_credentials （Transact-sql）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]傳回所有目標伺服器在設備中儲存的所有網路認證清單。 系統會針對控制項節點和每個計算節點列出結果。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|pdw_node_id|**int**|與節點相關聯的唯一數值識別碼。|  
|target_server_name|**Nvarchar （32）**|[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]將使用使用者名稱和密碼認證存取的目標伺服器 IP 位址。|  
|username|**Nvarchar （32）**|儲存密碼的使用者名稱。|  
|last_modified|**datetime**|上次修改認證之作業的日期時間。|  
  
## <a name="permissions"></a>權限  
 需要 VIEW SERVER 狀態。  
  
## <a name="general-remarks"></a>一般備註  
 這個動態管理檢視的索引鍵是*pdw_node_id*加*target_server_name*。  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲動態管理 Views &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
