---
title: "catalog.master_properties (SSISDB 資料庫) | Microsoft Docs"
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 00bfa716-5390-48e3-b30c-d954d5e0be47
caps.latest.revision: "3"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 28f72cd6a5ea50bdc310d89bf16dbe498e06a638
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="catalogmasterproperties-ssisdb-database"></a>catalog.master_properties (SSISDB 資料庫)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

顯示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out Master 的屬性。

|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|property_name|**nvarchar(256)**|相應放大主要屬性的名稱。|  
|property_value|**nvarchar(max)**|相應放大主要屬性的值。|

## <a name="remarks"></a>備註
這個檢視會顯示每個相應放大主要屬性的資料列。 這個檢視會顯示的屬性包括：

|屬性名稱|Description|  
|-------------------|-----------------| 
|**CLUSTER_LOGDB_SERVER**|記錄資料庫所在的 SQL Server。|
|**LAST_ONLINE_TIME**|Scale Out Master 上次上線的時間。|
|**MACHINE_IP**|電腦的 IP。|
|**MACHINE_NAME**|電腦的名稱。|
|**MASTER_ADDRESS**|Scale Out Master 的端點。|
|**MASTER_SERVICE_PORT**|Scale Out Master 端點中的埠。|
|**SSLCERT_THUMBPRINT**|Scale Out Master 憑證的指紋。|

## <a name="permissions"></a>Permissions
Public 資料庫角色的所有成員都擁有此檢視的讀取權限。 
