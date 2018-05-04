---
title: sys.numbered_procedure_parameters (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/10/2016
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
- numbered_procedure_parameters_TSQL
- sys.numbered_procedure_parameters_TSQL
- numbered_procedure_parameters
- sys.numbered_procedure_parameters
dev_langs:
- TSQL
helpviewer_keywords:
- sys.numbered_procedure_parameters catalog view
ms.assetid: a441d46d-1f30-41c2-8d94-e9442f59786e
caps.latest.revision: 20
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: d3e039a298e3bad8e76d76f9d81b065fa1b21c9a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sysnumberedprocedureparameters-transact-sql"></a>sys.numbered_procedure_parameters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對編號程序的每個參數，各包含一個資料列。 當您建立編號的預存程序時，基本程序的編號為 1。 後續所有程序則為 2 號、3 號等，依此類推。 **sys.numbered_procedure_parameters**包含所有後續程序，2 的參數定義和更新版本。 這份檢視不會顯示基本預存程序 (編號 = 1) 的參數。 基本預存程序類似於未編號的預存程序。 因此，以表示其參數[sys.parameters (TRANSACT-SQL)](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)。  
  
> [!IMPORTANT]  
>  編號程序已被取代。 不再使用編號程序。 當編譯使用這份目錄檢視的查詢時，會引發 DEPRECATION_ANNOUNCEMENT 事件。  
  
> [!NOTE]  
>  編號程序並不支援 XML 和 CLR 參數。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|這個參數所屬物件的識別碼。|  
|**procedure_number**|**smallint**|這個程序在物件內的編號，大於或等於 2。|  
|**name**|**sysname**|參數的名稱。 內是唯一的**procedure_number**。|  
|**parameter_id**|**int**|參數的識別碼。 內是唯一的**procedure_number**。|  
|**system_type_id**|**tinyint**|參數系統類型的識別碼。|  
|**user_type_id**|**int**|參數的類型識別碼 (如使用者所定義)。|  
|**max_length**|**smallint**|參數的最大長度 (以位元組為單位)。<br /><br /> -1 = 資料行的資料類型是 varchar(max)、nvarchar(max) 或 varbinary(max)。|  
|**有效位數**|**tinyint**|如果是以數值為基礎，便是參數的有效位數；否則，便是 0。|  
|**scale**|**tinyint**|如果是以數值為基礎，便是參數的小數位數；否則，便是 0。|  
|**is_output**|**bit**|1 = 參數是輸出 (或傳回)；否則，便是 0。|  
|**is_cursor_ref**|**bit**|1 = 參數是一個資料指標參考參數。|  
  
> [!NOTE]  
>  編號程序並不支援 XML 和 CLR 參數。  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [物件目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目錄檢視 &#40;。TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
