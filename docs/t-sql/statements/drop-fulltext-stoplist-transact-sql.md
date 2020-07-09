---
title: DROP FULLTEXT STOPLIST (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_FULLTEXT_STOPLIST_TSQL
- DROP FULLTEXT STOPLIST
dev_langs:
- TSQL
helpviewer_keywords:
- DROP FULLTEXT STOPLIST statement
- stoplists [full-text search]
- full-text search [SQL Server], stoplists
- full-text search [SQL Server], stopwords
- stopwords [full-text search]
ms.assetid: 3ee2a2bb-1dfb-4e7c-90e9-9d917cd84a15
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 48111db11e943f6a1e306f290e48e318579a99f1
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85766334"
---
# <a name="drop-fulltext-stoplist-transact-sql"></a>DROP FULLTEXT STOPLIST (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

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
 *stoplist_name*  
 這是資料庫中全文檢索停用字詞表的名稱。  
  
## <a name="remarks"></a>備註  
 如果有任何全文檢索索引參考所卸除的全文檢索停用字詞表，DROP FULLTEXT STOPLIST 就會失敗。  
  
## <a name="permissions"></a>權限  
 若要卸除停用字詞表，則需要具有此停用字詞表的 DROP 權限或是 **db_owner** 或 **db_ddladmin** 固定資料庫角色中的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會卸除名為 `myStoplist` 的全文檢索停用字詞表。  
  
```  
DROP FULLTEXT STOPLIST myStoplist;  
```  
  
## <a name="see-also"></a>另請參閱  
 [ALTER FULLTEXT STOPLIST &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-stoplist-transact-sql.md)   
 [CREATE FULLTEXT STOPLIST &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md)   
 [sys.fulltext_stoplists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql.md)   
 [sys.fulltext_stopwords &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md)  
  
  
