---
title: catalog.master_properties (SSISDB 資料庫) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.component: system-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 00bfa716-5390-48e3-b30c-d954d5e0be47
caps.latest.revision: 3
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c48f9e25d0a662f5f1f756b16b7f3edbe361de29
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="catalogmasterproperties-ssisdb-database"></a>catalog.master_properties (SSISDB 資料庫)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

顯示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out Master 的屬性。

|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|property_name|**nvarchar(256)**|相應放大主要屬性的名稱。|  
|property_value|**nvarchar(max)**|相應放大主要屬性的值。|

## <a name="remarks"></a>Remarks
這個檢視會顯示每個相應放大主要屬性的資料列。 這個檢視會顯示的屬性包括：

|屬性名稱|描述|  
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
