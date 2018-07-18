---
title: sys.time_zone_info & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/27/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 7
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 252def1ce861b926a6c8a990a3cbf10b22eb83f6
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "37984920"
---
# <a name="systimezoneinfo-transact-sql"></a>sys.time_zone_info & Amp;#40;transact-SQL&AMP;#41;
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  傳回支援的時區資訊。 在電腦上安裝所有的時區會儲存在下列登錄區：  
`KEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Time Zones`。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Windows 標準格式的時區名稱。 比方說， **cen。澳洲標準時間**或是**歐洲中部標準時間**。|  
|**current_utc_offset**|**nvarchar(12)**|目前的 UTC 的位移。 例如， **+ 01:00**或是 **-07:00**。|  
|**is_currently_dst**|**bit**|如果目前觀察日光節約時間，則為 true。|  
  
## <a name="see-also"></a>另請參閱  
 [GETUTCDATE &#40;Transact SQL&#41;](../../t-sql/functions/getutcdate-transact-sql.md)   
 [AT TIME ZONE &#40;Transact-SQL&#41;](../../t-sql/queries/at-time-zone-transact-sql.md)   
 [日期和時間資料類型與函式 &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)   
 [伺服器範圍組態目錄檢視&#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/server-wide-configuration-catalog-views-transact-sql.md)  
