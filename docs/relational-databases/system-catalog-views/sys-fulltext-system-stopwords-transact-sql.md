---
title: "sys.fulltext_system_stopwords (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.fulltext_system_stopwords_TSQL
- fulltext_system_stopwords
- fulltext_system_stopwords_TSQL
- sys.fulltext_system_stopwords
dev_langs: TSQL
helpviewer_keywords:
- stoplists [full-text search]
- sys.fulltext_system_stopwords catalog view
- full-text search [SQL Server], stopwords
- stopwords [full-text search]
ms.assetid: 487de53f-c637-4d78-85f6-fef5e768cd0c
caps.latest.revision: "19"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 20d1cc02e15d1c8c221f8d75005da504dfaf5b17
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="sysfulltextsystemstopwords-transact-sql"></a>sys.fulltext_system_stopwords (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  提供系統停用字詞表的存取權。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**停用字詞**|**nvarchar （64)**|要針對停用字詞比對進行考量的詞彙。|  
|**language_id**|**int**|語言的地區設定識別碼 (LCID)。 這個 LCID 是用於斷詞。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>請參閱＜  
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [物件目錄檢視 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [sys.fulltext_stoplists &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql.md)   
 [sys.fulltext_stopwords &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md)   
 [設定及管理全文檢索搜尋的停用字詞與停用字詞表](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)  
  
  
