---
title: "sys.syslanguages (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-compatibility-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.syslanguages
- sys.syslanguages_TSQL
- syslanguages
- syslanguages_TSQL
dev_langs: TSQL
helpviewer_keywords:
- syslanguages system table
- sys.syslanguages compatibility view
ms.assetid: f216d1cd-997c-42f0-a737-abbdfcd88383
caps.latest.revision: "37"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 5d0a0b2a001f40b8884faa1c8c22415708ba377f
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="syssyslanguages-transact-sql"></a>sys.syslanguages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中的每種語言，各包含一個資料列。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|langid|**smallint**|唯一語言識別碼。|  
|dateformat|**nchar(3)**|日期的順序，例如 DMY。|  
|datefirst|**tinyint**|每週第一天：1 代表星期一，2 代表星期二，依此類推，7 則代表星期日。|  
|升級|**int**|保留供系統使用。|  
|name|**sysname**|官方語言名稱，例如 Fran&#xE7;ais。|  
|alias|**sysname**|替代語言名稱，例如 French。|  
|months|**nvarchar(372)**|以逗號分隔的清單，依一月至十二月的順序列出完整長度的月份名稱，每個名稱最多可有 20 個字元。|  
|shortmonths|**nvarchar(132)**|以逗號分隔的清單，依一月至十二月的順序列出簡短的月份名稱，每個名稱最多可有 9 個字元。|  
|days|**nvarchar(217)**|以逗號分隔的清單，依星期一至星期日的順序列出各日的名稱，每個名稱最多可有 30 個字元。|  
|lcid|**int**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] 語言的 Windows 地區設定識別碼|  
|msglangid|**smallint**|[!INCLUDE[ssDE](../../includes/ssde-md.md)] 訊息群組識別碼。|  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 包含下列已安裝的語言。  
  
|英文名稱|Windows LCID|[!INCLUDE[ssDE](../../includes/ssde-md.md)] 訊息群組識別碼|  
|---------------------|------------------|-----------------------------------------|  
|英文|1033|1033|  
|德文|1031|1031|  
|法文|1036|1036|  
|日文|1041|1041|  
|丹麥文|1030|1030|  
|西班牙文|3082|3082|  
|義大利文|1040|1040|  
|荷蘭文|1043|1043|  
|挪威文|2068|2068|  
|葡萄牙文|2070|2070|  
|芬蘭文|1035|1035|  
|瑞典文|1053|1053|  
|捷克文|1029|1029|  
|匈牙利文|1038|1038|  
|波蘭文|1045|1045|  
|羅馬尼亞文|1048|1048|  
|克羅埃西亞文|1050|1050|  
|斯洛伐克文|1051|1051|  
|斯洛維尼亞文|1060|1060|  
|希臘文|1032|1032|  
|保加利亞文|1026|1026|  
|俄文|1049|1049|  
|土耳其文|1055|1055|  
|英式英文|2057|1033|  
|愛沙尼亞文|1061|1061|  
|拉脫維亞文|1062|1062|  
|立陶宛文|1063|1063|  
|巴西文|1046|1046|  
|繁體中文|1028|1028|  
|韓文|1042|1042|  
|簡體中文|2052|2052|  
|阿拉伯文|1025|1025|  
|泰文|1054|1054|  
  
## <a name="see-also"></a>請參閱＜  
 [相容性檢視 &#40;TRANSACT-SQL &#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)   
 [將系統資料表對應至系統檢視 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)  
  
  
