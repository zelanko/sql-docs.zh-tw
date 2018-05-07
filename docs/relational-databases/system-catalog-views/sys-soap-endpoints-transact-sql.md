---
title: sys.soap_endpoints (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- soap_endpoints_TSQL
- sys.soap_endpoints
- soap_endpoints
- sys.soap_endpoints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.soap_endpoints catalog view
ms.assetid: f50dcbfc-02ed-4a19-9c07-c78a5a1b3224
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 7f3af00bccbef87dd6390c5421b8d625e4b6ed42
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="syssoapendpoints-transact-sql"></a>sys.soap_endpoints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 針對伺服器中存放 SOAP 類型裝載的每個端點，各包含一個資料列。 在此檢視中的每個資料列，沒有對應的資料列具有相同**endpoint_id**中**sys.http_endpoints**目錄執行 HTTP 組態中繼資料的檢視。  
  
 
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**< 繼承的資料行 >**||如需這個檢視所繼承的資料行的清單，請參閱[sys.endpoints &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md)。|  
|**is_sql_language_enabled**|**bit**|指定 1 = BATCHES = ENABLED 選項，表示該端點可以有特定的 SQL 批次。|  
|**wsdl_generator_procedure**|**nvarchar(776)**|實作這個方法之預存程序的三部份名稱。<br /><br /> 方法的名稱必須遵循三部分的語法。 一部分、二部分及四部分的名稱皆不可使用。|  
|**default_database**|**sysname**|DATABASE = 選項中所給定的預設資料庫名稱。<br /><br /> 指定 NULL = DEFAULT。|  
|**default_namespace**|**nvarchar(384)**|指定命名空間中的預設命名空間 = 選項，或 'http://tempuri.org' 如果改為指定預設值。|  
|**default_result_schema**|**tinyint**|SCHEMA = 選項的預設值。<br /><br /> 0 = NONE<br /><br /> 1 = STANDARD|  
|**default_result_schema_desc**|**nvarchar(60)**|SCHEMA = 選項的預設值描述。<br /><br /> 無<br /><br /> STANDARD|  
|**is_xml_charset_enforced**|**bit**|已指定 0 = CHARACTER_SET = SQL 選項。<br /><br /> 已指定 1 = CHARACTER_SET = XML 選項。|  
|**is_session_enabled**|**bit**|已指定 0 = SESSION = DISABLE 選項。<br /><br /> 已指定 1 = SESSION = ENABLED 選項。|  
|**session_timeout**|**int**|在 SESSION_TIMEOUT = 選項中指定的值。|  
|**login_type**|**nvarchar(60)**|這個端點所接受的驗證種類。<br /><br /> WINDOWS<br /><br /> MIXED|  
|**header_limit**|**int**|SOAP 標頭所能接受的最大值。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [端點目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)   
 [目錄檢視 &#40;。TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
