---
description: 'sys. edge_constraints (Transact-sql) '
title: sys. edge_constraints (Transact-sql) |Microsoft Docs
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
ms.openlocfilehash: 7ceea1b9ad0c7995240187518522633de4ace1c9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88377834"
---
# <a name="sysedge_constraints-transact-sql"></a>sys. edge_constraints (Transact-sql) 
[!INCLUDE[sqlserver2019](../../includes/applies-to-version/sqlserver2019.md)]

針對做為邊緣條件約束的每個物件，各包含一個資料列。 
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**\<Columns inherited from sys.objects>**||如需此視圖所繼承之資料行的清單，請參閱 [sys. objects &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)。|  
|**is_disabled**|**bit**|1 = 邊緣條件約束為 disbled。<br /><br /> 0 = 已啟用邊緣條件約束。|  
|**is_not_trusted**|**bit**|1 = 系統尚未驗證邊緣條件約束。<br /><br /> 0 = 邊緣條件約束已由系統驗證。|  
|**delete_referential_action**|**tinyint**|此邊緣條件約束上定義的參考動作。<br /><br />0 = 沒有動作。|  
|**delete_referential_action_desc**|**nvarchar(60)**|此邊緣條件約束上定義之參考動作的描述。<br /><br />NO_ACTION|  
|**is_system_named**|**bit**|1 = 邊緣條件約束名稱是由系統所產生。<br /><br />0 = 邊緣條件約束名稱是由使用者提供。|  
  
## <a name="permissions"></a>權限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [物件目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查詢 SQL Server 系統目錄 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
