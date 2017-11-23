---
title: "ALTER FULLTEXT STOPLIST (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
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
- ALTER FULLTEXT STOPLIST
- ALTER_FULLTEXT_STOPLIST_TSQL
dev_langs: TSQL
helpviewer_keywords:
- stoplists [full-text search]
- full-text search [SQL Server], stoplists
- ALTER FULLTEXT STOPLIST statement
- full-text search [SQL Server], stopwords
- stopwords [full-text search]
ms.assetid: f6ad87d5-6a34-435a-8456-8244947c5c83
caps.latest.revision: "37"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 20947c0331f9713a937e0a7de8efb1f2fc9f753c
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="alter-fulltext-stoplist-transact-sql"></a>ALTER FULLTEXT STOPLIST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  在目前資料庫的預設全文檢索停用字詞表中插入或刪除停用字詞。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
ALTER FULLTEXT STOPLIST stoplist_name  
{   
        ADD [N] 'stopword' LANGUAGE language_term    
  | DROP   
    {  
        'stopword' LANGUAGE language_term   
      | ALL LANGUAGE language_term   
      | ALL  
     }  
;  
```  
  
## <a name="arguments"></a>引數  
 *s*  
 這是要改變的停用字詞表名稱。 *s*最多可有 128 個字元。  
  
 **'** *停用字詞* **'**  
 這是可能在指定語言中具有語言含意之文字的字串，或是沒有語言含意的 Token。 *停用字詞*限制為最大 token 的長度 （64 個字元）。 停用字詞可以指定為 Unicode 字串。  
  
 語言*language_term*  
 指定的語言與*停用字詞*已加入或卸除。  
  
 *language_term*可以指定為字串、 整數或十六進位值對應到語言的地區設定識別碼 (LCID)，如下所示：  
  
|格式|Description|  
|------------|-----------------|  
|字串|*language_term*對應至**別名**中的資料行值[sys.syslanguages (TRANSACT-SQL)](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)相容性檢視。 字串必須括在單引號中**'***language_term***'**。|  
|Integer|*language_term*是語言的 LCID。|  
|十六進位|*language_term* 0x 後面接著 LCID 的十六進位值。 十六進位值不能超出 8 位數，開頭的零也包括在內。 如果這個值是雙位元組字集 (DBCS) 格式，SQL Server 會將它轉換成 Unicode。|  
  
 新增**'***停用字詞***'**語言*language_term*  
 將指定語言的語言的停用字詞表的停用字詞*language_term*。  
  
 如果語言的關鍵字和 LCID 值的指定組合在 STOPLIST 中不是唯一的，將會傳回錯誤。  如果此 LCID 值未對應到註冊的語言，將會產生錯誤。  
  
 卸除 { **'***停用字詞***'**語言*language_term* |所有語言*language_term* |所有}  
 卸除停用字詞表中的停用字詞。  
  
 **'** *停用字詞* **'**語言*language_term*  
 卸除指定的語言指定的停用字詞*language_term*。  
  
 所有語言*language_term*  
 卸除所有指定的語言之停用字詞*language_term*。  
  
 ALL  
 卸除停用字詞表中的所有停用字詞。  
  
## <a name="remarks"></a>備註  
 CREATE FULLTEXT STOPLIST 僅支援相容性層級 100 和更高層級。 若為相容性層級 80 和 90，系統停用字詞表就一定會指派給資料庫。  
  
## <a name="permissions"></a>Permissions  
 若要將停用字詞表指定為資料庫的預設停用字詞表，則需要 ALTER DATABASE 權限。 若要變更停用字詞表，則必須停用字詞表的擁有者或成員資格**db_owner**或**db_ddladmin**固定資料庫角色。  
  
## <a name="examples"></a>範例  
 下列範例會變更名為 `CombinedFunctionWordList` 的停用字詞表，加入 'en' 一字 (先針對西班牙文，再針對法文)。  
  
```  
ALTER FULLTEXT STOPLIST CombinedFunctionWordList ADD 'en' LANGUAGE 'Spanish';  
ALTER FULLTEXT STOPLIST CombinedFunctionWordList ADD 'en' LANGUAGE 'French';  
```  
  
## <a name="see-also"></a>請參閱＜  
 [建立全文檢索停用字詞表 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md)   
 [卸除全文檢索停用字詞表 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-fulltext-stoplist-transact-sql.md)   
 [設定及管理全文檢索搜尋停用字詞與停用字詞表](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   
 [sys.fulltext_stoplists &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql.md)   
 [sys.fulltext_stopwords &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md)   
 [設定及管理全文檢索搜尋的停用字詞與停用字詞表](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)  
  
  
