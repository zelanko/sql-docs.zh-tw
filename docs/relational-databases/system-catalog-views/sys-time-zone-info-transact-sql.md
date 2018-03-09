---
title: "sys.time_zone_info (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 09/12/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Data Warehouse
- SQL Server (starting with 2016)
f1_keywords:
- sys.time_zone_info
- sys.time_zone_info_TSQL
- time_zone_info
- time_zone_info_TSQL
helpviewer_keywords:
- sys.time_zone_info system table
ms.assetid: 3f51a9a4-75f8-4a11-9552-8bf6118b68da
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b4d893e468c2d9820506bb4be18de8c8fbb6dd28
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="systimezoneinfo-transact-sql"></a>sys.time_zone_info (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  傳回支援的時區資訊。 在電腦上安裝所有的時區會儲存在下列的登錄區：  
`KEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Time Zones`。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Windows 標準格式的時區名稱。 例如， **cen。澳大利亞標準時間**或**歐洲中部標準時間**。|  
|**current_utc_offset**|**nvarchar （12)**|目前的 UTC 的位移。 例如， **+ 01:00**或**-07:00**。|  
|**is_currently_dst**|**bit**|如果目前觀察日光節約時間，則為 true。|  
  
## <a name="see-also"></a>請參閱＜  
 [GETUTCDATE &#40;TRANSACT-SQL &#41;](../../t-sql/functions/getutcdate-transact-sql.md)   
 [TIME ZONE &AMP;#40;TRANSACT-SQL &#41;](../../t-sql/queries/at-time-zone-transact-sql.md)   
 [日期和時間資料類型和函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)   
 [伺服器範圍組態目錄檢視 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/server-wide-configuration-catalog-views-transact-sql.md)  
  
  
