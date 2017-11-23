---
title: "sys.sysaltfiles (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-compatibility-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.sysaltfiles_TSQL
- sys.sysaltfiles
- sysaltfiles_TSQL
- sysaltfiles
dev_langs: TSQL
helpviewer_keywords:
- sysaltfiles system table
- sys.sysaltfiles compatibility view
ms.assetid: 698dec23-5336-4108-87a5-f8e407f8da09
caps.latest.revision: "35"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e79cd2d5a4e0833af0fe03e2787e065606f7b105
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="syssysaltfiles-transact-sql"></a>sys.sysaltfiles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在特殊情況之下，包含對應於資料庫中之檔案的資料列。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
||  
|-|  
|**適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [目前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))。|  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**fileid**|**smallint**|檔案識別碼。 每個資料庫的這個項目都是唯一的。|  
|**groupid**|**smallint**|檔案群組識別碼。|  
|**大小**|**int**|檔案大小 (以 8 KB 頁面為單位)。|  
|**maxsize**|**int**|最大檔案大小 (以 8 KB 頁面為單位)。<br /><br /> 0 = 不成長。<br /><br /> -1 = 檔案會成長到磁碟已滿。<br /><br /> 268435456 = 記錄檔可以成長到最大 2 TB 的大小。<br /><br /> 注意： 升級以無限的記錄檔案大小的資料庫將會報告記錄檔的大小上限-1。|  
|**成長**|**int**|資料庫的成長大小。<br /><br /> 0 = 不成長。 隨著狀態值而不同，它可以是頁數或檔案大小百分比。 如果**狀態**是 0x100000，**成長**是百分比檔案大小; 否則它是頁數。|  
|**status**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**效能**|**int**|已保留。|  
|**dbid**|**smallint**|這個檔案所屬的資料庫之資料庫識別碼。|  
|**name**|**sysname**|檔案的邏輯名稱。|  
|**檔名**|**nvarchar （260)**|實體裝置的名稱。 其中包括檔案的完整路徑。|  
  
## <a name="see-also"></a>請參閱＜  
 [將系統資料表對應至系統檢視 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [相容性檢視 &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
