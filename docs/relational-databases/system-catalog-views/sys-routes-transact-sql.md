---
title: sys.routes (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/30/2018
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- routes
- routes_TSQL
- sys.routes
- sys.routes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.routes catalog view
ms.assetid: 8fc65915-8bd6-425b-95d9-6a8468cb1e48
caps.latest.revision: 33
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 88893373067090d120f75c7b7f74d9cefdf213b9
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sysroutes-transact-sql"></a>sys.routes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  這份目錄檢視會針對每個路由，各包含一個資料列。 Service Broker 使用路由來尋找服務的網路位址。   

[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|路由的名稱，它在資料庫中是唯一的。 不是 NULLABLE。|  
|**route_id**|**int**|路由的識別碼。 不是 NULLABLE。|  
|**principal_id**|**int**|擁有該路由的資料庫主體識別碼。 NULLABLE。|  
|**remote_service_name**|**nvarchar(256)**|遠端服務的名稱。 NULLABLE。|  
|**broker_instance**|**nvarchar(128)**|主控遠端服務的 Broker 識別碼。 NULLABLE。|  
|**lifetime**|**datetime**|路由到期的日期和時間。 請注意，此值不使用當地的時區。 此值會顯示 UTC 格式的到期時間。 NULLABLE。|  
|**address**|**nvarchar(256)**|Service Broker 傳送遠端服務訊息至的網路位址。 NULLABLE。 SQL 資料庫 Managed 執行個體，必須是本機位址。|  
|**mirror_address**|**nvarchar(256)**|位址中所指定的伺服器之鏡像夥伴網路位址。 NULLABLE。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
  
