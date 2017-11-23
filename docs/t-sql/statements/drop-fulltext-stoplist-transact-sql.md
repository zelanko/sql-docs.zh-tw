---
title: "卸除全文檢索停用字詞表 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_FULLTEXT_STOPLIST_TSQL
- DROP FULLTEXT STOPLIST
dev_langs: TSQL
helpviewer_keywords:
- DROP FULLTEXT STOPLIST statement
- stoplists [full-text search]
- full-text search [SQL Server], stoplists
- full-text search [SQL Server], stopwords
- stopwords [full-text search]
ms.assetid: 3ee2a2bb-1dfb-4e7c-90e9-9d917cd84a15
caps.latest.revision: "24"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bf761059b932045cffe635fb169684718e612402
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="drop-fulltext-stoplist-transact-sql"></a>DROP FULLTEXT STOPLIST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的資料庫中卸除全文檢索停用字詞表。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
> [!IMPORTANT]  
>  CREATE FULLTEXT STOPLIST 僅支援相容性層級 100 和更高層級。 若為相容性層級 80 和 90，系統停用字詞表就一定會指派給資料庫。  
  
## <a name="syntax"></a>語法  
  
```  
  
DROP FULLTEXT STOPLIST stoplist_name  
;  
```  
  
## <a name="arguments"></a>引數  
 *s*  
 這是資料庫中全文檢索停用字詞表的名稱。  
  
## <a name="remarks"></a>備註  
 如果有任何全文檢索索引參考所卸除的全文檢索停用字詞表，DROP FULLTEXT STOPLIST 就會失敗。  
  
## <a name="permissions"></a>Permissions  
 若要卸除停用字詞表，則需要具有卸除或權限停用字詞表中的成員資格**db_owner**或**db_ddladmin**固定資料庫角色。  
  
## <a name="examples"></a>範例  
 下列範例會卸除名為 `myStoplist` 的全文檢索停用字詞表。  
  
```  
DROP FULLTEXT STOPLIST myStoplist;  
```  
  
## <a name="see-also"></a>請參閱＜  
 [ALTER FULLTEXT STOPLIST &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-fulltext-stoplist-transact-sql.md)   
 [建立全文檢索停用字詞表 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md)   
 [sys.fulltext_stoplists &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql.md)   
 [sys.fulltext_stopwords &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md)  
  
  
