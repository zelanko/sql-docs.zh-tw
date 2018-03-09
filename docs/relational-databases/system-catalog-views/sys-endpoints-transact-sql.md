---
title: "sys.endpoints (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- endpoints
- sys.endpoints
- endpoints_TSQL
- sys.endpoints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.endpoints catalog view
ms.assetid: e6dafa4e-e47e-43ec-acfc-88c0af53c1a1
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1ded68aefc2121f651b9005fe3e75b64ec80dc0c
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="sysendpoints-transact-sql"></a>sys.endpoints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對在系統建立的每個端點，各包含一個資料列。 SYSTEM 端點一定只有一個。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|端點的名稱。 在伺服器中，這是唯一的。 不可為 Null。|  
|**endpoint_id**|**int**|端點的識別碼。 在伺服器中，這是唯一的。 識別碼小於 65536 的端點是系統端點。 不可為 Null。|  
|**principal_id**|**int**|建立和擁有這個端點的伺服器主體識別碼。 可為 Null。|  
|**通訊協定**|**tinyint**|端點通訊協定。<br /><br /> 1 = HTTP<br /><br /> 2 = TCP<br /><br /> 3 = 具名管道<br /><br /> 4 = 共用記憶體<br /><br /> 5 = 虛擬介面配接器 (VIA)<br /><br /> 不可為 Null。|  
|**protocol_desc**|**nvarchar （60)**|端點通訊協定的描述。 NULLABLE。 為下列其中一個值：<br /><br /> **HTTP**<br /><br /> **TCP**<br /><br /> **NAMED_PIPES**<br /><br /> **SHARED_MEMORY**<br /><br /> **透過**附註： 透過通訊協定已被取代。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]|  
|**型別**|**tinyint**|端點裝載類型。<br /><br /> 1 = SOAP<br /><br /> 2 = TSQL<br /><br /> 3 = SERVICE_BROKER<br /><br /> 4 = DATABASE_MIRRORING<br /><br /> 不可為 Null。|  
|**type_desc**|**nvarchar （60)**|端點裝載類型的描述。 可為 Null。 為下列其中一個值：<br /><br /> **SOAP**<br /><br /> **TSQL**<br /><br /> **SERVICE_BROKER**<br /><br /> **DATABASE_MIRRORING**|  
|**狀態**|**tinyint**|端點狀態。<br /><br /> 0 = STARTED，接聽和處理要求。<br /><br /> 1 = STOPPED，接聽但不處理要求。<br /><br /> 2 = DISABLED，不接聽<br /><br /> 預設狀態為 1。 可為 Null。|  
|**state_desc**|**nvarchar （60)**|端點狀態的描述。<br /><br /> STARTED = 接聽和處理要求。<br /><br /> STOPPED = 接聽但不處理要求。<br /><br /> DISABLED = 不接聽。<br /><br /> 預設狀態是 STOPPED。<br /><br /> 可為 Null。|  
|**is_admin_endpoint**|**bit**|指出端點是否作為管理使用。<br /><br /> 0 = 非管理端點。<br /><br /> 1 = 端點是管理端點。<br /><br /> 不可為 Null。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>請參閱＜  
 [端點目錄檢視 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
