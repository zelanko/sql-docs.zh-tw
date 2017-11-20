---
title: "catalog.master_properties （SSISDB 資料庫） |Microsoft 文件"
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 00bfa716-5390-48e3-b30c-d954d5e0be47
caps.latest.revision: 3
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: cd1366409f9fb0af271b26fad3b8b911f99acc06
ms.openlocfilehash: 0fcbdca57c7764eaec758d2ad9ef3ab8675a3a9b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/08/2017

---
# <a name="catalogmasterproperties-ssisdb-database"></a>catalog.master_properties （SSISDB 資料庫）
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

顯示的屬性[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]出主要刻度。

|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|property_name|**nvarchar(256)**|主要屬性的擴充名稱。|  
|property_value|**nvarchar(max)**|擴充主要屬性的值。|

## <a name="remarks"></a>備註
此檢視會顯示針對每個擴充的主要屬性的資料列。 這個檢視會顯示的屬性包括：

|屬性名稱|Description|  
|-------------------|-----------------| 
|**CLUSTER_LOGDB_SERVER**|在中，找出記錄資料庫，SQL Server。|
|**LAST_ONLINE_TIME**|當標尺出主要是線上上次的時間。|
|**MACHINE_IP**|電腦的 IP。|
|**MACHINE_NAME**|電腦的名稱。|
|**MASTER_ADDRESS**|標尺出主要端點。|
|**MASTER_SERVICE_PORT**|中的標尺出主要端點的通訊埠。|
|**SSLCERT_THUMBPRINT**|標尺出主要憑證的指紋。|

## <a name="permissions"></a>Permissions
Public 資料庫角色的所有成員擁有都讀取權限，此檢視。 

