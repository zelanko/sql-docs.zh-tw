---
title: "使用 NEAR 搜尋靠近另一個單字的字詞 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-search"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "單字搜尋 [全文檢索搜尋]"
  - "NEAR 選項 [全文檢索搜尋]"
  - "片語搜尋 [全文檢索搜尋]"
  - "鄰近搜尋 [全文檢索搜尋]"
  - "全文檢索搜尋 [SQL Server], 鄰近搜尋"
  - "全文檢索查詢 [SQL Server], 鄰近"
  - "查詢 [全文檢索搜尋], 鄰近"
ms.assetid: 87520646-4865-49ae-8790-f766b80a41f3
caps.latest.revision: 65
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 63
---
# 使用 NEAR 搜尋靠近另一個單字的字詞
  您可以在 [CONTAINS](../../t-sql/queries/contains-transact-sql.md) 述詞或 [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) 函數中使用鄰近字詞 (NEAR)，以便搜尋彼此接近的單字或片語。 您也可以指定分隔第一個和最後一個搜尋詞彙之非搜尋詞彙的數目上限。 此外，您也可以依任何順序或是您所指定的順序來搜尋單字或片語。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 支援舊版的[泛型鄰近字詞](#Generic_NEAR) (目前已被取代) 和[自訂鄰近字詞](#Custom_NEAR) ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中的新功能)。  
  
##  <a name="Custom_NEAR"></a> 自訂相近詞彙  
 自訂相近詞彙導入下列新功能：  
  
-   您可以指定分隔第一個和最後一個搜尋字詞之非搜尋字詞的數目上限 (或「最大距離」)，以便構成符合項目。  
  
-   如果您指定了詞彙的數目上限，也可以指定符合項目必須按照指定的順序包含搜尋詞彙。  
  
 若要成為符合項目，文字字串必須：  
  
-   以其中一個指定的搜尋詞彙為開頭，並且以其中一個指定的其他搜尋詞彙為結尾。  
  
-   包含所有指定的搜尋詞彙。  
  
-   出現在第一個和最後一個搜尋詞彙之間的非搜尋詞彙 (包括停用字詞) 數目必須小於或等於最大距離 (如果有指定的話)。  
  
 基本語法如下：  
  
 NEAR (  
  
 {  
  
 *search_term* [ ,…*n* ]  
  
 |  
  
 (*search_term* [ ,…*n* ] ) [, <maximum_distance> [, <match_order> ] ]  
  
 }  
  
 )  
  
> [!NOTE]  
>  如需 <custom_proximity_term> 語法的詳細資訊，請參閱 [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)。  
  
 例如，您可以搜尋與 'Smith' 距離兩個詞彙以內的 'John'，如下所示：  
  
```  
CONTAINS(column_name, 'NEAR((John, Smith), 2)')  
```  
  
 符合的部分字串範例包括 "`John Jacob Smith`" 和 "`Smith, John`"。 "`John Jones knows Fred Smith`" 字串包含三個中介非搜尋詞彙，所以它不是符合項目。  
  
 若要要求按照指定的順序尋找詞彙，您會將範例相近詞彙變更為 `NEAR((John, Smith),2, TRUE).`。這樣就會搜尋與 "`John`" 距離兩個詞彙以內的 "`Smith`"，但是只有當 "`John`" 在 "`Smith`" 前面時才符合。 在由左至右閱讀的語言 (例如英文) 中，符合的字串範例為 "`John Jacob Smith`"。  
  
 請注意，若為由右至左閱讀的語言 (例如阿拉伯文或希伯來文)，全文檢索引擎就會按照反向順序套用指定的詞彙。 此外，[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的 [物件總管] 會自動反轉以由右至左書寫語言所指定之單字的顯示順序。  
  
> [!NOTE]  
>  如需詳細資訊，請參閱本主題稍後的＜[有關鄰近搜尋的其他考量](#Additional_Considerations)＞。  
  
### 最大距離的測量方式  
 特定的最大距離 (例如 10 或 25) 會決定給定字串中出現在第一個和最後一個搜尋詞彙之間的非搜尋詞彙 (包含停用字詞) 數目。 例如，`NEAR((dogs, cats, "hunting mice"), 3)` 會傳回下列資料列，其中非搜尋詞彙的總數是三 ("`enjoy`"、"`but`" 和 "`avoid`")：  
  
 "`Cats` `enjoy` `hunting mice``, but avoid` `dogs``.`"  
  
 相同的相近詞彙不會傳回下列資料列，因為四個非搜尋詞彙 ("`enjoy`"、"`but`"、"`usually`" 和 "`avoid`") 超過了最大距離：  
  
 "`Cats` `enjoy` `hunting mice``, but usually avoid` `dogs``.`"  
  
### 結合自訂相近詞彙與其他詞彙  
 您可以結合自訂相近詞彙與其他某些詞彙。 您可以使用 AND (&)、OR (|) 或 AND NOT (&!) 來結合自訂鄰近字詞與其他自訂鄰近字詞、不可分割的字詞或前置字詞。 例如：  
  
-   CONTAINS('NEAR((*term1*,*term2*),5) AND *term3*')  
  
-   CONTAINS('NEAR((*term1*,*term2*),5) OR *term3*')  
  
-   CONTAINS('NEAR((*term1*,*term2*),5) AND NOT *term3*')  
  
-   CONTAINS('NEAR((*term1*,*term2*),5) AND NEAR((*term3*,*term4*),2)')  
  
-   CONTAINS('NEAR((*term1*,*term2*),5) OR NEAR((*term3*,*term4*),2, TRUE)')  
  
 例如，  
  
```  
CONTAINS(column_name, 'NEAR((term1, term2), 5, TRUE) AND term3')  
```  
  
 您無法結合自訂鄰近字詞與泛型鄰近字詞 (*term1* NEAR *term2*)、衍生字詞 (ISABOUT …) 或加權字詞 (FORMSOF …)。  
  
### 範例：使用自訂相近詞彙  
 下列範例會在 `Production.Document` 範例資料庫的 `AdventureWorks2012` 資料表中搜尋包含與 "bracket" 一字位於相同文件中之 "reflector" 一字的所有文件摘要。  
  
```  
SELECT DocumentNode, Title, DocumentSummary  
FROM Production.Document AS DocTable   
INNER JOIN CONTAINSTABLE(Production.Document, Document,  
  'NEAR(bracket, reflector)' ) AS KEY_TBL  
  ON DocTable.DocumentNode = KEY_TBL.[KEY]  
WHERE KEY_TBL.RANK > 50  
ORDER BY KEY_TBL.RANK DESC;  
GO  
```  
  
 [本主題內容](#top)  
  
##  <a name="Additional_Considerations"></a> 鄰近搜尋的其他考量  
 本節將討論同時影響泛型和自訂鄰近搜尋的考量：  
  
-   搜尋詞彙的重疊項目  
  
     所有鄰近搜尋都只會尋找非重疊項目。 搜尋詞彙的重疊項目絕對不會成為符合項目。 例如，請考慮下列相近詞彙，它會按照此順序搜尋最大距離為兩個詞彙的 "`A`" 和 "`AA`"：  
  
    ```  
    CONTAINS(column_name, 'NEAR((A,AA),2, TRUE')  
    ```  
  
     可能的符合項目為 "`AAA`"、"`A.AA`" 和 "`A..AA`"。 只包含 "`AA`" 的資料列則不符合。  
  
    > [!NOTE]  
    >  您可以指定重疊的詞彙，例如 `NEAR("mountain bike", "bike trails")` 或 `(NEAR(comfort*, comfortable), 5)`。 指定重疊的詞彙會增加可能的符合項目排列，因而增加查詢的複雜性。 如果您大量指定這類重疊的詞彙，查詢可能會耗盡資源並失敗。 如果發生這種情況，請簡化查詢，然後再試一次。  
  
-   泛型 NEAR 和自訂 NEAR (不論是否指定最大距離) 都表示詞彙之間的邏輯距離，而非詞彙之間的絕對距離。 例如，在某個段落中，不同片語或句子內的詞彙會比相同片語或句子內的詞彙被視為距離較遠，不論其實際距離為何都一樣，不過前提是它們都互不相關。 同樣地，不同段落中的詞彙則被視為距離更遠。 如果某個符合項目跨越句子、段落或章節的結尾，用於排列文件等級的間距會分別增加 8、128 或 1024。  
  
-   相近詞彙對於 CONTAINSTABLE 函數排列等級的影響  
  
     在 CONTAINSTABLE 函數中使用 NEAR 時，文件的叫用次數相對於其長度以及每次叫用中第一個和最後一個搜尋詞彙之間的距離就會影響每份文件的等級。 對於泛型相近詞彙而言，如果符合的搜尋詞彙距離 >50 個邏輯詞彙，針對文件傳回的等級就是 0。 若為沒有指定整數做為最大距離的自訂相近詞彙，只包含間距 >100 個邏輯詞彙之叫用的文件將收到的等級為 0。 如需自訂鄰近搜尋等級的詳細資訊，請參閱[限制 RANK 的搜索結果](../../relational-databases/search/limit-search-results-with-rank.md)。  
  
-   [轉換非搜尋字] 伺服器選項  
  
     如果您在鄰近搜尋中指定停用字詞，則 [轉換非搜尋字] 的值會影響 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理停用字詞的方式。 如需詳細資訊，請參閱[轉換非搜尋字伺服器組態選項](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md)。  
  
 [本主題內容](#top)  
  
##  <a name="Generic_NEAR"></a> 已被取代的泛型相近詞彙  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 建議您使用[自訂鄰近字詞](#Custom_NEAR)。  
  
 泛型鄰近字詞表示指定的搜尋字詞必須全部都出現在同一份文件中，才會傳回符合項目，而不論搜尋字詞之間的非搜尋字詞數目 (「距離」) 為何。 基本語法如下：  
  
 { *search_term* { NEAR | ~ } *search_term* } [ ,…*n* ]  
  
 例如，在下列範例中，'fox' 和 'chicken' 這兩個字必須同時出現 (按照任何順序)，才會產生符合項目：  
  
-   `CONTAINS(column_name, 'fox NEAR chicken')`  
  
-   `CONTAINSTABLE(table_name, column_name, 'fox ~ chicken')`  
  
> [!NOTE]  
>  如需 <generic_proximity_term> 語法的相關資訊，請參閱 [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)。  
  
 如需詳細資訊，請參閱本主題稍後的＜[有關鄰近搜尋的其他考量](#Additional_Considerations)＞。  
  
### 結合泛型相近詞彙與其他詞彙  
 您可以使用 AND (&)、OR (|) 或 AND NOT (&!) 來結合泛型鄰近字詞與其他泛型鄰近字詞、不可分割的字詞或前置字詞。 例如：  
  
```  
CONTAINSTABLE (Production.ProductDescription,  
   Description,   
   '(light NEAR aluminum) OR  
   (lightweight NEAR aluminum)'  
)  
```  
  
 您無法結合泛型相近詞彙與自訂相近詞彙 (例如 `NEAR((term1,term2),5)`)、加權詞彙 (ISABOUT …) 或衍生詞彙 (FORMSOF …)。  
  
### 範例：使用泛型相近詞彙  
 下列範例會使用泛型相近詞彙來搜尋與 "bracket" 一字位於相同文件中的 "reflector" 一字。  
  
```  
USE AdventureWorks2012;  
GO  
  
SELECT DocumentNode, Title, DocumentSummary  
FROM Production.Document AS DocTable INNER JOIN  
  CONTAINSTABLE(Production.Document, Document,  
  '(reflector NEAR bracket)' ) AS KEY_TBL  
  ON DocTable.DocumentNode = KEY_TBL.[KEY]  
ORDER BY KEY_TBL.RANK DESC;  
GO  
```  
  
 請注意，將 CONTAINSTABLE 中的詞彙顛倒也可以得到相同的結果：  
  
```  
CONTAINSTABLE(Production.Document, Document, '(bracket NEAR reflector)' ) AS KEY_TBL  
```  
  
 您可以使用 (~) 字元來取代前面查詢中的 NEAR 關鍵字，也可得到相同的結果：  
  
```  
CONTAINSTABLE(Production.Document, Document, '(reflector ~ bracket)' ) AS KEY_TBL  
```  
  
 搜尋條件中可以指定兩個以上單字或片語。 例如，您可以撰寫：  
  
```  
CONTAINSTABLE(Production.Document, Document, '(reflector ~ bracket ~ installation)' ) AS KEY_TBL  
```  
  
 這表示 "reflector" 必須與 "bracket" 位於相同的文件中，而且 "bracket" 必須與 "installation" 位於相同的文件中。  
  
 [本主題內容](#top)  
  
## 另請參閱  
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [使用全文檢索搜尋進行查詢](../../relational-databases/search/query-with-full-text-search.md)   
 [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)  
  
  