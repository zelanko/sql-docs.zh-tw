---
title: sys.plan_guides & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.planguides_TSQL
- plan_guides
- sys.planguides
- plan_guides_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.plan_guides catalog view
ms.assetid: 3dde0397-ef6f-4b3f-8250-3f25584eb62b
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 75d95fbe9c289eab419360bef35263b41930c9f7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47696477"
---
# <a name="sysplanguides-transact-sql"></a>sys.plan_guides (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  針對資料庫中每份計畫指南，各包含一個資料列。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**plan_guide_id**|**int**|資料庫中計畫指南的唯一識別碼。|  
|**name**|**sysname**|計畫指南的名稱。|  
|**create_date**|**datetime**|建立計畫指南的日期和時間。|  
|**modify_date**|**Datetime**|上次修改計畫指南的日期。|  
|**sys.indexes**|**bit**|1 = 計畫指南已停用。<br /><br /> 0 = 計畫指南已啟用。|  
|**query_text**|**nvarchar(max)**|建立計畫指南的查詢文字。|  
|**scope_type**|**tinyint**|識別計畫指南的範圍。<br /><br /> 1 = OBJECT<br /><br /> 2 = SQL<br /><br /> 3 = TEMPLATE|  
|**scope_type_desc**|**nvarchar(60)**|計畫指南範圍的描述。<br /><br /> OBJECT<br /><br /> SQL<br /><br /> TEMPLATE|  
|**scope_object_id**|**整數**|定義計畫指南範圍之物件的 object_id (如果範圍是 OBJECT)。<br /><br /> 如果計畫指南的範圍不是 OBJECT，則為 NULL。|  
|**scope_batch**|**nvarchar(max)**|如果批次文字**scope_type**為 SQL。<br /><br /> NULL (如果批次類型不是 SQL)。<br /><br /> 如果是 NULL， **scope_type**是 SQL、 windows 7 **query_text**套用。|  
|**parameters**|**nvarchar(max)**|定義與計畫指南相關參數清單的字串。<br /><br /> NULL = 沒有一個參數清單與計畫指南相關。|  
|**提示**|**nvarchar(max)**|與計畫指南相關的 OPTION 子句提示。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sp_create_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
  
