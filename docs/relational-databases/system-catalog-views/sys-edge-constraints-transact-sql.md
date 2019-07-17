---
title: sys.edge_constraints (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 09/17/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.edge_constraints
- edge_constraints
- SQL Graph
- edge_constraints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.edge_constraints catalog view
ms.assetid: 0f782d2f-7126-46ab-85b7-bcba44862231
author: shkale-msft
ms.author: shkale
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5dc2e47c49dc9d639489426fceab0b848c9def3e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68079322"
---
# <a name="sysedgeconstraints-transact-sql"></a>sys.edge_constraints & Amp;#40;transact-SQL&AMP;#41;
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx.md](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

包含每個物件，會有邊緣條件約束的一個資料列。 
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**\<從 sys.objects 繼承的資料行 >**||如需這個檢視所繼承的資料行的清單，請參閱 < [j &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)。|  
|**is_disabled**|**bit**|1 = 條件約束停用的邊緣。<br /><br /> 0 = 已啟用條件約束的邊緣。|  
|**is_not_trusted**|**bit**|1 = 條件約束尚未驗證系統的邊緣。<br /><br /> 0 = 系統已通過驗證條件約束的邊緣。|  
|**delete_referential_action**|**tinyint**|此邊緣條件約束定義的參考動作。<br /><br />0 = 沒有動作。|  
|**delete_referential_action_desc**|**nvarchar(60)**|此邊緣條件約束定義的參考動作的描述。<br /><br />NO_ACTION|  
|**is_system_named**|**bit**|1 = 條件約束名稱已由系統產生的邊緣。<br /><br />0 = 條件約束名稱由使用者所提供的邊緣。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [物件目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查詢 SQL Server 系統目錄常見問題集](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
