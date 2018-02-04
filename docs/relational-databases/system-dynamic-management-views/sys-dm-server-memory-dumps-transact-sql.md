---
title: "sys.dm_server_memory_dumps (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
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
- sys.dm_server_memory_dumps_TSQL
- dm_server_memory_dumps_TSQL
- dm_server_memory_dumps
- sys.dm_server_memory_dumps
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_server_memory_dumps dynamic management view
ms.assetid: 41782719-f54d-4e11-941a-c050c7576e23
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7db1d81b38cea74eb61c38f29218fb68a6a1b1fa
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmservermemorydumps-transact-sql"></a>sys.dm_server_memory_dumps (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 所產生的每個記憶體傾印檔，各傳回一個資料列。 使用此動態管理檢視疑難排解潛在問題。  
 
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**filename**|**nvarchar(256)**|記憶體傾印檔的路徑和名稱。 不可為 null。|  
|**creation_time**|**datetimeoffset(7)**|建立檔案的日期與時間。 不可為 null。|  
|**size_in_bytes**|**bigint**|檔案大小 (以位元組為單位)。 可為 Null。|  
  
## <a name="general-remarks"></a>一般備註  
 傾印類型可以是迷你傾印、所有執行緒傾印或完整傾印。 檔案的副檔名為 .mdmp。  
  
## <a name="security"></a>Security  
 傾印檔可能包含敏感性資訊。 若要保護敏感性資訊，您可以使用存取控制清單 (ACL) 來限制這些檔案的存取權，或將這些檔案複製到具有存取限制的資料夾。 例如，在將偵錯檔傳回至 Microsoft 支援服務之前，建議您先移除任何敏感或機密資訊。  
  
### <a name="permissions"></a>Permissions  
 需要 VIEW SERVER STATE 權限。  
  
  
