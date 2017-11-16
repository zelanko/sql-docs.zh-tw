---
title: "使用 NEAR 搜尋靠近另一個單字的字詞 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-search
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: TSQL
helpviewer_keywords:
- word searches [full-text search]
- NEAR option [full-text search]
- phrase searches [full-text search]
- proximity searches [full-text search]
- full-text search [SQL Server], proximity searches
- full-text queries [SQL Server], proximity
- queries [full-text search], proximity
ms.assetid: 87520646-4865-49ae-8790-f766b80a41f3
caps.latest.revision: "65"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 81230587be4efd864fb2ec3958a1473db8de2e53
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="search-for-words-close-to-another-word-with-near"></a>使用 NEAR 搜尋靠近另一個單字的字詞
  您可以在 [CONTAINS](../../t-sql/queries/contains-transact-sql.md) 述詞或 [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) 函式中使用「鄰近字詞」 **NEAR**，以便搜尋彼此接近的單字或片語。 
  
##  <a name="Custom_NEAR"></a> NEAR 的概觀  
**NEAR** 具有下列功能：  
-   您可以指定分隔第一個和最後一個搜尋詞彙之非搜尋詞彙的數目上限。

-   您可以依任何順序來搜尋單字或片語，或依特定順序來搜尋單字或片語。
  
-   您可以指定分隔第一個和最後一個搜尋字詞之非搜尋字詞的數目上限 (或「最大距離」)，以便構成符合項目。  

-   如果您指定了詞彙的數目上限，也可以指定符合項目必須按照指定的順序包含搜尋詞彙。

 
 若要成為符合項目，文字字串必須：  
  
-   以其中一個指定的搜尋詞彙為開頭，並且以其中一個指定的其他搜尋詞彙為結尾。  
  
-   包含所有指定的搜尋詞彙。  
  
-   出現在第一個和最後一個搜尋詞彙之間的非搜尋詞彙 (包括停用字詞) 數目必須小於或等於最大距離 (如果指定最大距離的話)。  
  
## <a name="syntax-of-near"></a>NEAR 的語法
**NEAR** 的基本語法如下：  

``` 
 NEAR (  
  
 {  
  
 *search_term* [ ,…*n* ]  
  
 |  
  
 (*search_term* [ ,…*n* ] ) [, <maximum_distance> [, <match_order> ] ]  
  
 }  
  
 )  
```

如需語法的詳細資訊，請參閱 [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)。  

## <a name="examples"></a>範例
### <a name="example-1"></a>範例 1
 例如，您可以搜尋與 'Smith' 距離兩個詞彙以內的 'John'，如下所示：  
  
```tsql
... CONTAINS(column_name, 'NEAR((John, Smith), 2)')
```  
  
 符合的部分字串範例包括 "`John Jacob Smith`" 和 "`Smith, John`"。 "`John Jones knows Fred Smith`" 字串包含三個中介非搜尋詞彙，所以它不是符合項目。  
  
 若要要求按照指定的順序尋找詞彙，您會將範例相近詞彙變更為 `NEAR((John, Smith),2, TRUE).` 。這樣就會搜尋與 "`John`" 距離兩個詞彙以內的 "`Smith`"，但是只有當 "`John`" 在 "`Smith`" 前面時才符合。 在由左至右閱讀的語言 (例如英文) 中，符合的字串範例為 "`John Jacob Smith`"。  
  
 請注意，若為由右至左閱讀的語言 (例如阿拉伯文或希伯來文)，全文檢索引擎就會按照反向順序套用指定的詞彙。 此外， [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的 [物件總管] 會自動反轉以由右至左書寫語言所指定之單字的顯示順序。   

### <a name="example-2"></a>範例 2
 下列範例會在 `Production.Document` 範例資料庫的 `AdventureWorks` 資料表中搜尋包含與 "bracket" 一字位於相同文件中之 "reflector" 一字的所有文件摘要。  
  
```tsql
SELECT DocumentNode, Title, DocumentSummary  
FROM Production.Document AS DocTable   
INNER JOIN CONTAINSTABLE(Production.Document, Document,  
  'NEAR(bracket, reflector)' ) AS KEY_TBL  
  ON DocTable.DocumentNode = KEY_TBL.[KEY]  
WHERE KEY_TBL.RANK > 50  
ORDER BY KEY_TBL.RANK DESC;  
GO  
``` 
 
## <a name="how-maximum-distance-is-measured"></a>最大距離的測量方式  
 特定的最大距離 (例如 10 或 25) 會決定給定字串中出現在第一個和最後一個搜尋詞彙之間的非搜尋詞彙 (包含停用字詞) 數目。 例如， `NEAR((dogs, cats, "hunting mice"), 3)` 會傳回下列資料列，其中非搜尋詞彙的總數是三 ("`enjoy`"、"`but`" 和 "`avoid`")：  
  
 "`Cats` `enjoy` `hunting mice``, but avoid` `dogs``.`"  
  
 相同的相近詞彙不會傳回下列資料列，因為四個非搜尋詞彙 ("`enjoy`"、"`but`"、"`usually`" 和 "`avoid`") 超過了最大距離：  
  
 "`Cats` `enjoy` `hunting mice``, but usually avoid` `dogs``.`"  
  
## <a name="combine-near-with-other-terms"></a>合併使用 NEAR 與其他詞彙  
 您可以合併使用 NEAR 與一些其他詞彙。 您可以使用 AND (&)、OR (|) 或 AND NOT (&!) 來結合自訂鄰近字詞與其他自訂鄰近字詞、不可分割的字詞或前置字詞。 例如：  
  
-   CONTAINS('NEAR((*term1*,*term2*),5) AND *term3*')  
  
-   CONTAINS('NEAR((*term1*,*term2*),5) OR *term3*')  
  
-   CONTAINS('NEAR((*term1*,*term2*),5) AND NOT *term3*')  
  
-   CONTAINS('NEAR((*term1*,*term2*),5) AND NEAR((*term3*,*term4*),2)')  
  
-   CONTAINS('NEAR((*term1*,*term2*),5) OR NEAR((*term3*,*term4*),2, TRUE)')  
  
 例如，  
  
```  
CONTAINS(column_name, 'NEAR((term1, term2), 5, TRUE) AND term3')  
```  
  
 您無法合併使用 NEAR、衍生詞彙 (ISABOUT …) 或加權詞彙 (FORMSOF …)。  
  
##  <a name="Additional_Considerations"></a> 深入了解鄰近搜尋  
   
-   搜尋詞彙的重疊項目  
  
     所有鄰近搜尋都只會尋找非重疊項目。 搜尋詞彙的重疊項目絕對不會成為符合項目。 例如，請考慮下列相近詞彙，它會按照此順序搜尋最大距離為兩個詞彙的 "`A`" 和 "`AA`"：  
  
    ```  
    CONTAINS(column_name, 'NEAR((A,AA),2, TRUE')  
    ```  
  
     可能的符合項目為 "`AAA`"、"`A.AA`" 和 "`A..AA`"。 只包含 "`AA`" 的資料列則不符合。  
  
    > [!NOTE]  
    >  您可以指定重疊的詞彙，例如 `NEAR("mountain bike", "bike trails")` 或 `(NEAR(comfort*, comfortable), 5)`。 指定重疊的詞彙會增加可能的符合項目排列，因而增加查詢的複雜性。 如果您大量指定這類重疊的詞彙，查詢可能會耗盡資源並失敗。 如果發生這種情況，請簡化查詢，然後再試一次。  
  
-   NEAR (不論是否指定最大距離) 表示詞彙之間的邏輯距離，而非詞彙之間的絕對距離。 例如，在某個段落中，不同片語或句子內的詞彙會比相同片語或句子內的詞彙被視為距離較遠，不論其實際距離為何都一樣，不過前提是它們都互不相關。 同樣地，不同段落中的詞彙則被視為距離更遠。 如果某個符合項目跨越句子、段落或章節的結尾，用於排列文件等級的間距會分別增加 8、128 或 1024。  
  
-   相近詞彙對於 CONTAINSTABLE 函數排列等級的影響  
  
    在 CONTAINSTABLE 函數中使用 NEAR 時，文件的叫用次數相對於其長度以及每次叫用中第一個和最後一個搜尋詞彙之間的距離就會影響每份文件的等級。 對於泛型相近詞彙而言，如果符合的搜尋詞彙距離 >50 個邏輯詞彙，針對文件傳回的等級就是 0。 若為沒有指定整數做為最大距離的自訂相近詞彙，只包含間距 >100 個邏輯詞彙之叫用的文件將收到的等級為 0。 如需自訂鄰近搜尋等級的詳細資訊，請參閱[限制 RANK 的搜索結果](../../relational-databases/search/limit-search-results-with-rank.md)。  
  
-   [轉換非搜尋字] 伺服器選項  
  
     如果您在鄰近搜尋中指定停用字詞，則 [轉換非搜尋字] 的值會影響 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理停用字詞的方式。 如需詳細資訊，請參閱 [轉換非搜尋字伺服器組態選項](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md)。   
  
## <a name="see-also"></a>另請參閱  
 [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)  
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [使用全文檢索搜尋進行查詢](../../relational-databases/search/query-with-full-text-search.md)   
