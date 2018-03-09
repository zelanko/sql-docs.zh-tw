---
title: "sys.endpoint_webmethods (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
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
- sys.endpoint_webmethods_TSQL
- sys.endpoint_webmethods
- endpoint_webmethods_TSQL
- sys.http_soap_methods_TSQL
- endpoint_webmethods
- sys.http_soap_methods
dev_langs:
- TSQL
helpviewer_keywords:
- sys.endpoint_webmethods catalog view
ms.assetid: 7dad0cf6-eafa-47cf-98cc-75ba8d3c7959
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 93053b36893b6812128d2bb397a656d395f839af
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
---
# <a name="sysendpointwebmethods-transact-sql"></a>sys.endpoint_webmethods (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 包含定義在啟用 SOAP 之 HTTP 端點的一個資料列 FOR EACH SOAP 方法。 Endpoint_id 和命名空間的資料行組合是唯一的。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|endpoint_id|**int**|定義 webmethod 的端點識別碼。|  
|命名空間|**nvarchar(384)**|webmethod 的命名空間。|  
|method_alias|**nvarchar （64)**|方法的別名。<br /><br /> 注意：[!INCLUDE[tsql](../../includes/tsql-md.md)]識別碼接受 WSDL 方法名稱中不合法的字元。<br /><br /> 這個別名用來將端點之 WSDL 描述所顯示的名稱，對應至當叫用 webmethod 時所呼叫的實際基礎 [!INCLUDE[tsql](../../includes/tsql-md.md)] 可執行物件。|  
|object_name|**nvarchar(776)**|根據 NAME = 選項的指定，重新導向 webmethod 所至的物件名稱。 名稱的組件會以句號 （.）、 分隔，而使用方括號分隔`[``]`。<br /><br /> 根據 WSDL 選項的指定，物件名稱必須是三部分名稱。|  
|result_schema|**tinyint**|決定哪一個 (如果有的話) XSD 會隨同回應被傳回的選項。<br /><br /> 0 = 無<br /><br /> 1 = 標準<br /><br /> 2 = 預設值|  
|result_schema_desc|**nvarchar （60)**|決定哪一個 (如果有的話) XSD 會隨同回應被傳回的選項描述。<br /><br /> 無<br /><br /> STANDARD<br /><br /> DEFAULT|  
|result_format|**tinyint**|決定回應中的結果如何格式化的選項。<br /><br /> 1 = ALL_RESULTS<br /><br /> 2 = ROWSETS_ONLY<br /><br /> 3 = 無|  
|result_format_desc|**nvarchar （60)**|決定回應中的結果如何格式化的選項描述。<br /><br /> ALL_RESULTS<br /><br /> ROWSETS_ONLY<br /><br /> 無|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>請參閱  
 [端點目錄檢視 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
