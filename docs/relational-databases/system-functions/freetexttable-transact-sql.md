---
description: FREETEXTTABLE (Transact-SQL)
title: FREETEXTTABLE (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- FREETEXTTABLE_TSQL
- FREETEXTTABLE
dev_langs:
- TSQL
helpviewer_keywords:
- search conditions [SQL Server], meaning matches
- meaning matches [full-text search]
- FREETEXTTABLE function (Transact-SQL)
- ranked results [full-text search]
- column searches [full-text search]
ms.assetid: 4523ae15-4260-40a7-a53c-8df15e1fee79
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 83aa956f8a9a9421cdbc411856be78af272f1fa6
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97482514"
---
# <a name="freetexttable-transact-sql"></a>FREETEXTTABLE (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  這是 SELECT 語句之 [from 子句](../../t-sql/queries/from-transact-sql.md) 中使用的函數 [!INCLUDE[tsql](../../includes/tsql-md.md)] ，可在包含以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 字元為基礎之資料類型的全文檢索索引資料行上執行全文檢索搜尋。 此函數會傳回零個、一個或多個資料列的資料表，這些資料行包含的值符合指定之 *freetext_string* 中文字的意義，而不只是確切的用語。 FREETEXTTABLE 參考方式就如同一般資料表名稱一樣。  
  
 FREETEXTTABLE 適用于與 [FREETEXT &#40;transact-sql&#41;](../../t-sql/queries/freetext-transact-sql.md)相同的比對類型，  
  
 使用 FREETEXTTABLE 的查詢會針對每個資料列傳回一個相關次序值 (RANK) 和全文檢索索引鍵 (KEY)，如下所示：  
  
> [!NOTE]  
>  如需有關 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所支援全文檢索搜尋形式的資訊，請參閱[使用全文檢索搜尋進行查詢](../../relational-databases/search/query-with-full-text-search.md)。  
  
 (https://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag)) 。 |  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
FREETEXTTABLE (table , { column_name | (column_list) | * }   
          , 'freetext_string'   
     [ , LANGUAGE language_term ]   
     [ , top_n_by_rank ] )  
```  
  
## <a name="arguments"></a>引數  
 *table*  
 這是已標示全文檢索查詢的資料表名稱。 *資料表* 或 *視圖* 可以是一個、兩個或三部分的資料庫物件名稱。 當查詢檢視時，只能包含一個全文檢索索引基底資料表。  
  
 *資料表* 不能指定伺服器名稱，也不能在針對連結伺服器的查詢中使用。  
  
 *column_name*  
 這是在 FROM 子句中指定之資料表一個或多個全文檢索索引資料行的名稱。 資料行可為以下類型：**char**、**varchar**、**nchar**、**nvarchar**、**text**、**ntext**、**image**、**xml**、**varbinary** 或 **varbinary(max)** 。  
  
 *column_list*  
 指出您可以指定多個資料行，各資料行用逗號分隔。 *column_list* 必須括在括號中。 除非已指定 *language_term*，否則 *column_list* 之所有資料行的語言都必須相同。  
  
 \*  
 指定所有已登錄全文檢索搜尋的資料行都應該用來搜尋指定的 *freetext_string*。 除非指定了 *language_term* ，否則資料表中所有全文檢索索引資料行的語言都必須相同。  
  
 *freetext_string*  
 這是要在 *column_name* 中搜尋的文字。 您可以輸入任何文字，其中包括單字、片語或句子。 在全文檢索索引中找到任何詞彙或任何詞彙的各種形式，都會產生相符項目。  
  
 不同于 CONTAINS 搜尋條件中，AND 是關鍵字，當使用於 *freetext_string* 時，' AND ' 會被視為非搜尋字或 [停用字詞](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)，而且將會被捨棄。  
  
 不允許使用 WEIGHT、FORMSOF、萬用字元、NEAR 和其他語法。 *freetext_string* 會經過斷字、進行詞幹分析，然後進行同義字檢查。  
  
 LANGUAGE *language_term*  
 這是查詢利用其資源來斷詞、分析詞幹，以及移除同義字和停用字詞的語言。 這個參數是選擇性的，可以指定成對應於語言地區設定識別碼 (LCID) 的字串、整數或十六進位值。 如果指定 *language_term*，系統就會將它所代表的語言套用至搜尋條件的所有項。 如果未指定任何值，就會使用資料行全文檢索語言。  
  
 如果不同語言的文件當做二進位大型物件 (BLOB) 一起儲存在單一資料行中，給定文件的地區設定識別碼 (LCID) 會判斷要建立其內容索引所使用的語言。 查詢這類資料行時，指定 *LANGUAGE language_term* 可能會提高相符的機率。  
  
 當指定為字串時，*language_term* 會對應到 [sys.syslanguages &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md) 相容性檢視表中的 **alias** 資料行值。  字串必須以單引號括住，如 '*language_term*'。 當指定為整數時，*language_term* 是用於識別語言的實際 LCID。 當指定為十六進位值時，*language_term* 是 0x，後面接著 LCID 的十六進位值。 十六進位值不能超出 8 位數，開頭的零也包括在內。  
  
 如果這個值是雙位元組字集 (DBCS) 格式，[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將其轉換成 Unicode。  
  
 如果指定的語言無效，或尚未安裝對應於這個語言的資源，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 就會傳回錯誤。 若要使用中性語言資源，請將 0x0 指定為 *language_term*。  
  
 *top_n_by_rank*  
 指定只傳回 *n* 個最高等級的相符專案（以遞減順序）。 只有在指定了整數值 *n* 時才適用。 如果結合 *top_n_by_rank* 與其他參數，則查詢所傳回的資料列數目會少於實際符合所有述詞的資料列數目。 *top_n_by_rank* 可讓您只重新叫用最相關的叫用來提高查詢效能。  
  
## <a name="remarks"></a>備註  
 全文檢索述詞與函數會在 FROM 述詞中隱含的單一資料表上處理。 若要在多個資料表上進行搜尋，請使用 FROM 子句中聯結的資料表，在兩個或多個資料表之產品的結果集上進行搜尋。  
  
 FREETEXTTABLE 使用與 FREETEXT 述詞相同的搜尋條件。  
  
 如同 CONTAINSTABLE，傳回的資料表具有名為 **KEY** 和 **RANK** 的資料行，這些資料行會在查詢中參考以取得適當的資料列，並使用資料列的排名值。  
  
## <a name="permissions"></a>權限  
 使用者必須具備指定的資料表或資料表中被參考的資料行之適當 SELECT 權限，才能叫用 FREETEXTTABLE。  
  
## <a name="examples"></a>範例  
  
### <a name="a-simple-example"></a>A. 簡單範例  
 下列範例會建立並填入兩個數據行的簡單資料表，並在其旗標中列出3個縣（市）和色彩。 它會建立並填入資料表上的全文檢索目錄和索引。 然後會示範 **FREETEXTTABLE** 語法。  
  
```  
CREATE TABLE Flags (Country nvarchar(30) NOT NULL, FlagColors varchar(200));  
CREATE UNIQUE CLUSTERED INDEX FlagKey ON Flags(Country);  
INSERT Flags VALUES ('France', 'Blue and White and Red');  
INSERT Flags VALUES ('Italy', 'Green and White and Red');  
INSERT Flags VALUES ('Tanzania', 'Green and Yellow and Black and Yellow and Blue');  
SELECT * FROM Flags;  
GO  
  
CREATE FULLTEXT CATALOG TestFTCat;  
CREATE FULLTEXT INDEX ON Flags(FlagColors) KEY INDEX FlagKey ON TestFTCat;  
GO   
  
SELECT * FROM Flags;  
SELECT * FROM FREETEXTTABLE (Flags, FlagColors, 'Blue');  
SELECT * FROM FREETEXTTABLE (Flags, FlagColors, 'Yellow');  
```  
  
### <a name="b-using-freetext-in-an-inner-join"></a>B. 在 INNER JOIN 中使用 FREETEXT  
 下列範例會傳回任何產品的描述和等級，其描述項合的意義 `high level of performance` 。  
  
```  
USE AdventureWorks2012;  
GO  
  
SELECT FT_TBL.Description  
    ,KEY_TBL.RANK  
FROM Production.ProductDescription AS FT_TBL   
    INNER JOIN FREETEXTTABLE(Production.ProductDescription,  
    Description,   
    'high level of performance') AS KEY_TBL  
ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
ORDER BY RANK DESC;  
GO  
```  
  
### <a name="c-specifying-language-and-highest-ranked-matches"></a>C. 指定語言和最高等級的相符項目  
 下列範例完全相同，並顯示 `LANGUAGE` *language_term* 和 *top_n_by_rank* 參數的用法。  
  
```  
USE AdventureWorks2012;  
GO  
  
SELECT FT_TBL.Description  
    ,KEY_TBL.RANK  
FROM Production.ProductDescription AS FT_TBL   
    INNER JOIN FREETEXTTABLE(Production.ProductDescription,  
    Description,   
    'high level of performance',  
    LANGUAGE N'English', 2) AS KEY_TBL  
ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
ORDER BY RANK DESC;  
GO  
```  
  
> [!NOTE]
>  使用 *top_n_by_rank* 參數不需要 LANGUAGE *language_term* 參數。  
  
## <a name="see-also"></a>另請參閱  
 [全文檢索搜尋使用者入門](../../relational-databases/search/get-started-with-full-text-search.md)   
 [建立及管理全文檢索目錄](../../relational-databases/search/create-and-manage-full-text-catalogs.md)   
 [CREATE FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [建立及管理全文檢索索引](../../relational-databases/search/create-and-manage-full-text-indexes.md)   
 [使用全文檢索搜尋進行查詢](../../relational-databases/search/query-with-full-text-search.md)   
 [建立全文檢索搜尋查詢 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-full-text-search-queries-visual-database-tools.md)   
 [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)   
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [FREETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/freetext-transact-sql.md)   
 [資料列集函數 &#40;Transact-sql&#41;](../../t-sql/functions/opendatasource-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)   
 [預先計算次序伺服器組態選項](../../database-engine/configure-windows/precompute-rank-server-configuration-option.md)  
  
