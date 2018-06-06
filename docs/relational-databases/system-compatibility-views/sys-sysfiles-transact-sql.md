---
title: sys.sysfiles (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-compatibility-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysfiles
- sys.sysfiles_TSQL
- sys.sysfiles
- sysfiles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysfiles system table
- sys.sysfiles compatibility view
ms.assetid: 3b47f38d-1cff-404d-89d3-9342c451c802
caps.latest.revision: 40
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 74db81ffa2764f3243a80b504df84b9f6ffd6ec5
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="syssysfiles-transact-sql"></a>sys.sysfiles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對資料庫中的每個檔案，各包含一個資料列。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**fileid**|**smallint**|每個資料庫的唯一檔案識別碼。|  
|**groupid**|**smallint**|檔案群組識別碼。|  
|**size**|**int**|檔案大小 (以 8KB 頁面為單位)。|  
|**maxsize**|**int**|最大檔案大小 (以 8 KB 頁面為單位)。<br /><br /> 0 = 不成長。<br /><br /> -1 = 檔案會成長到磁碟已滿。<br /><br /> 268435456 = 記錄檔可以成長到最大 2 TB 的大小。<br /><br /> 注意： 升級以無限的記錄檔案大小的資料庫將會報告記錄檔的大小上限-1。|  
|**成長**|**int**|資料庫的成長大小。 可以是頁數或檔案大小，根據值的百分比**狀態**。<br /><br /> 0 = 不成長。|  
|**status**|**int**|狀態位元**成長**(mb) 或 (kb) 中的值。<br /><br /> 0x2 = 磁碟檔。<br /><br /> 0x40 = 記錄檔。<br /><br /> 0x100000 = 成長。 這個值是一個百分比，不是頁數。|  
|**perf**|**int**|已保留。|  
|**name**|**sysname**|檔案的邏輯名稱。|  
|**filename**|**nvarchar(260)**|實體裝置的名稱。 其中包括檔案的完整路徑。|  
  
## <a name="see-also"></a>另請參閱  
 [將系統資料表對應至系統檢視表&#40;Transact SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [相容性檢視 &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
