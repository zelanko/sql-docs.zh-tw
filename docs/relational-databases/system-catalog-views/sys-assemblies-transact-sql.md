---
title: "m (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.assemblies
- assemblies_TSQL
- sys.assemblies_TSQL
- assemblies
dev_langs:
- TSQL
helpviewer_keywords:
- sys.assemblies catalog view
ms.assetid: e321753f-293f-42ab-b225-d118713df40b
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6e539377bf1c0d7c4060238baf26a152f02dbbdd
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="sysassemblies-transact-sql"></a>sys.assemblies (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  針對每個組件，各傳回一個資料列。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|組件的名稱。 在資料庫中，這是唯一的。|  
|**principal_id**|**int**|擁有這個組件之主體的識別碼。|  
|**assembly_id**|**int**|組件識別碼。 在資料庫中，這是唯一的。|  
|**clr_name**|**nvarchar(4000)**|將簡單名稱、版本號碼、文化、公開金鑰和組件架構加以編碼的標準字串。 這個值可以唯一識別 Common Language Runtime (CLR) 端的組件。|  
|**permission_set**|**tinyint**|組件的權限集合/安全性層級。<br /><br /> 1 = 安全存取<br /><br /> 2 = 外部存取<br /><br /> 3 = 不安全存取|  
|**permission_set_desc**|**nvarchar(60)**|組件的權限集合/安全層級描述。<br /><br /> SAFE_ACCESS<br /><br /> EXTERNAL_ACCESS<br /><br /> UNSAFE_ACCESS|  
|**is_visible**|**bit**|1 = 只要是註冊 [!INCLUDE[tsql](../../includes/tsql-md.md)] 進入點都看得到組件。<br /><br /> 0 = 組件是專供 Managed 呼叫端使用。 也就是說，組件會為資料庫中的其他組件提供內部實作。|  
|**create_date**|**datetime**|建立或登錄組件的日期。|  
|**modify_date**|**datetime**|修改組件的日期。|  
|**is_user_defined**|**bit**|指示組件的來源。<br /><br /> 0 = 系統定義的組件 (例如 Microsoft.SqlServer.Types **hierarchyid**資料類型)<br /><br /> 1 = 使用者定義的組件|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [CLR 組件目錄檢視 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/clr-assembly-catalog-views-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [ASSEMBLYPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/assemblyproperty-transact-sql.md)  
  
  
