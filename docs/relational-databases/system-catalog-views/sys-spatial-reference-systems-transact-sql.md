---
title: "sys.spatial_reference_systems (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- spatial_reference_systems_TSQL
- sys.spatial_reference_systems_TSQL
- sys.spatial_reference_systems
- spatial_reference_systems
dev_langs:
- TSQL
helpviewer_keywords:
- sys.spatial_reference_systems catalog view
- spatial_reference_systems
ms.assetid: 3c9bc120-67c3-463f-9e24-29fd623f25a0
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a4490cc6d28ee06193436de8b57cde8e7ac04402
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="sysspatialreferencesystems-transact-sql"></a>sys.spatial_reference_systems (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  列出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援的空間參考系統 (SRID)。  

  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|spatial_reference_id|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援的 SRID。|  
|authority_name|**nvarchar （128)**|SRID 的權威當局。|  
|authorized_spatial_reference_id|**int**|在名為授權單位所指定的 SRID **authority_name**。|  
|well_known_text|**nvarchar(4000)**|SRID 的 WKT 表示。|  
|unit_of_measure|**nvarchar （128)**|度量單位的名稱。|  
|unit_conversion_factor|**float**|以公尺為度量單位的長度。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
  
