---
title: dbo.sysdac_instances (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysdac_instances_TSQL
- sysdac_instances
- sysdac_instances_TSQL
- dbo.sysdac_instances
dev_langs:
- TSQL
helpviewer_keywords:
- dbo.sysdac_instances
- sysdac_instances
ms.assetid: 28285f3d-3889-439f-8b24-3bdef08e46b4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 049f3d0201957cfee5d7bc88301c6af97c0b6dcb
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51660678"
---
# <a name="data-tier-application-views---dbosysdacinstances"></a>資料層應用程式檢視-dbo.sysdac_instances
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  針對部署至 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體的每個資料層應用程式 (DAC) 執行階段，各顯示一個資料列。 sysdac_instances 屬於 msdb 資料庫中的 dbo 結構描述。 下表描述 [sysdac_instances] 檢視中的資料行。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|instance_id|**uniqueidentifier**|DAC 執行個體的識別碼。|  
|instance_name|**sysname**|部署 DAC 時指定之 DAC 執行個體的名稱。|  
|type_name|**sysname**|建立 DAC 封裝時指定之 DAC 的名稱。|  
|type_version|**nvarchar(64)**|建立 DAC 封裝時指定之 DAC 的版本。|  
|description|**nvarchar(4000)**|建立 DAC 封裝時寫入之 DAC 的描述。|  
|type_stream|**varbinary(max)**|包含 DAC 中之邏輯物件編碼表示法的位元資料流，例如，資料表和檢視表。|  
|date_created|**datetime**|建立 DAC 執行個體的日期和時間。|  
|created_by|**sysname**|建立 DAC 執行個體的登入。|  
|database_name|**sysname**|為 DAC 執行個體建立的資料庫名稱。|  
  
## <a name="remarks"></a>備註  
 DAC 包含 DAC 類型，這是應用程式所使用之邏輯資料層物件的定義，例如資料表和檢視表。 DAC 封裝是用來部署 DAC 的檔案。 DAC 封裝包含 DAC 類型中所有邏輯物件的表示。 DAC 封裝可以用來將一個或多個 DAC 的複本或執行個體部署至 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體。 從相同 DAC 封裝部署的每個 DAC 執行個體都共用相同的類型，但會被指派一個唯一的執行個體名稱和識別碼。  
  
## <a name="permissions"></a>Permissions  
 需要系統管理員 (sysadmin) 固定伺服器角色中的成員資格，才能檢視所有資料行。 Public 角色的成員可以檢視 instance_name、description 與 type_version 資料行。  
  
## <a name="see-also"></a>另請參閱  
 [資料層應用程式](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [資料層應用程式檢視&#40;Transact SQL&#41;](https://msdn.microsoft.com/library/0de01328-d7a6-4677-b7a0-dcd3098c23d4)  
  
  
