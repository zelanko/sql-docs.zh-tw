---
title: "sys.system_components_surface_area_configuration (TRANSACT-SQL) |Microsoft 文件"
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
- sys.system_components_surface_area_configuration_TSQL
- system_components_surface_area_configuration
- system_components_surface_area_configuration_TSQL
- sys.system_components_surface_area_configuration
dev_langs:
- TSQL
helpviewer_keywords:
- sys.system_components_surface_area_configuration catalog view
ms.assetid: d9920008-3387-4f9e-8f21-47473f2ba04f
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dbb274959c508b396419bb5597acb2fd6bfe5476
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
---
# <a name="syssystemcomponentssurfaceareaconfiguration-transact-sql"></a>sys.system_components_surface_area_configuration (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對可由介面區組態元件啟動或停用的每一個可執行檔系統物件，各傳回一個資料列。 如需詳細資訊，請參閱＜ [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md)＞。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**元件 _ 名稱**|**sysname**|元件名稱。 這將會有關鍵字定序 Latin1_General_CI_AS_KS_WS。 不能是 NULL。|  
|**database_name**|**sysname**|包含物件的資料庫。 這將會有關鍵字定序 Latin1_General_CI_AS_KS_WS。 必須是下列其中之一：<br /><br /> **master**<br /><br /> **msdb**<br /><br /> **mssqlsystemresource**|  
|**schema_name**|**sysname**|包含物件的結構描述。 這將會有關鍵字定序 Latin1_General_CI_AS_KS_WS。 不能是 NULL。|  
|**object_name**|**sysname**|物件的名稱。 這將會有關鍵字定序 Latin1_General_CI_AS_KS_WS。 不能是 NULL。|  
|**狀態**|**tinyint**|0 = 已停用<br /><br /> 1 = 已啟用|  
|**型別**|**char(2)**|物件類型。 可以是下列其中一項：<br /><br /> P = SQL_STORED_PROCEDURE<br /><br /> PC = CLR_STORED_PROCEDURE<br /><br /> FN = SQL_SCALAR_FUNCTION<br /><br /> FS = CLR_SCALAR_FUNCTION<br /><br /> FT = CLR_TABLE_VALUED_FUNCTION<br /><br /> IF = SQL_INLINE_TABLE_VALUED_FUNCTION<br /><br /> TF = SQL_TABLE_VALUED_FUNCTION<br /><br /> X = EXTENDED_STORED_PROCEDURE|  
|**type_desc**|**nvarchar （60)**|物件類型的易記名稱描述。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>請參閱  
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [安全性目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
