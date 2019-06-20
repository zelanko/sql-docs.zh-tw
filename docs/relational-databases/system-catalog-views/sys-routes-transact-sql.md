---
title: sys.routes (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 09/07/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 098ff2a0a3e4827a9d80c3955cc6f2689c3fa53e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62446425"
---
# <a name="sysroutes-transact-sql"></a>sys.routes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  這份目錄檢視會針對每個路由，各包含一個資料列。 Service Broker 使用路由來尋找服務的網路位址。   

|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|路由的名稱，它在資料庫中是唯一的。 不是 NULLABLE。|  
|**route_id**|**int**|路由的識別碼。 不是 NULLABLE。|  
|**principal_id**|**int**|擁有該路由的資料庫主體識別碼。 NULLABLE。|  
|**remote_service_name**|**nvarchar(256)**|遠端服務的名稱。 NULLABLE。|  
|**broker_instance**|**nvarchar(128)**|主控遠端服務的 Broker 識別碼。 NULLABLE。|  
|**lifetime**|**datetime**|路由到期的日期和時間。 請注意，此值不使用當地的時區。 此值會顯示 UTC 格式的到期時間。 NULLABLE。|  
|**address**|**nvarchar(256)**|Service Broker 傳送遠端服務訊息至的網路位址。 NULLABLE。 SQL Database 受控執行個體，位址必須是本機。|  
|**mirror_address**|**nvarchar(256)**|位址中所指定的伺服器之鏡像夥伴網路位址。 NULLABLE。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
  
