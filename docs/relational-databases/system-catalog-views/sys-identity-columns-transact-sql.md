---
title: sys.identity_columns (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- identity_columns
- sys.identity_columns
- sys.identity_columns_TSQL
- identity_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.identity_columns catalog view
ms.assetid: 97ee01e6-9c9e-4fd9-884b-68b4084669d5
caps.latest.revision: 44
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 21749d2f0f8f2db22399700031f17f4f2bc65132
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sysidentitycolumns-transact-sql"></a>sys.identity_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  針對每個識別欄位，各包含一個資料列。  
  
 **Sys.identity_columns**檢視繼承資料列從**sys.columns**檢視。 **Sys.identity_columns**檢視傳回的資料行中**sys.columns**  檢視中，再加上**seed_value**， **increment_value**， **last_value**，和**is_not_for_replication**資料行。 如需詳細資訊，請參閱[目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**\<資料行繼承自 sys.columns >**||**Sys.identity_columns**檢視會傳回所有資料行的**sys.columns**檢視。 另外亦將傳回以下所述的其他資料行。 如需資料行的描述， **sys.identity_columns**檢視繼承自**sys.columns**，請參閱[sys.columns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)。|  
|**seed_value**|**sql_variant**|這個識別欄位的初始值。 初始值的資料類型，與資料行本身的資料類型相同。|  
|**increment_value**|**sql_variant**|這個識別欄位的遞增值。 初始值的資料類型，與資料行本身的資料類型相同。|  
|**last_value**|**sql_variant**|這個識別欄位的最終值。 初始值的資料類型，與資料行本身的資料類型相同。|  
|**is_not_for_replication**|**bit**|識別欄位被宣告為 NOT FOR REPLICATION。|  
  
> [!NOTE]  
>  若要建立可用於多個資料表中或可在不參考任何資料表的情況下從應用程式進行呼叫的自動遞增數字，請參閱[序號](../../relational-databases/sequence-numbers/sequence-numbers.md)。  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [物件目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查詢 SQL Server 系統目錄常見問題集](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
