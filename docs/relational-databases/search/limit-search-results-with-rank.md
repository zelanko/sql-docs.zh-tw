---
title: 使用 RANK 限制搜索結果 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- row ranking [full-text search]
- relevance ranking values [full-text search]
- full-text search [SQL Server], rankings
- index rankings [full-text search]
- ranked results [full-text search]
- rankings [full-text search]
- per-row rank values [full-text search]
ms.assetid: 06a776e6-296c-4ec7-9fa5-0794709ccb17
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: bb7d238a3ff475fe47dbe652adab3cc49ca3a3b2
ms.sourcegitcommit: 03870f0577abde3113e0e9916cd82590f78a377c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/18/2019
ms.locfileid: "57973687"
---
# <a name="limit-search-results-with-rank"></a>限制 RANK 的搜索結果
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) 和 [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) 函數會傳回名為 RANK 的資料行，其中包含 0 到 1000 (順位值) 的序數值。 這些值的用途，在根據傳回資料列符合選取準則的程度予以分級。 等級值僅表示結果集中資料列相關性的相對順序，其值越低表示相關性越低。 實際的值並不重要，而且每次執行查詢後該值通常會不一樣。  
  
> [!NOTE]  
>  CONTAINS 與 FREETEXT 述詞不會傳回任何等級值。  
  
 符合搜尋條件的項目數通常會非常龐大。 若要防止 CONTAINSTABLE 或 FREETEXTTABLE 查詢傳回太多相符項目，請使用選擇性 *top_n_by_rank* 參數，以便僅傳回資料列的子集。 *top_n_by_rank* 是整數值 *n*，其中指定依遞減順序僅傳回 *n* 個最高等級的相符項目。 如果結合 *top_n_by_rank* 與其他參數，則查詢所傳回的資料列數目會少於實際符合所有述詞的資料列數目。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將依照等級來排序相符項目，並且最多只傳回指定的資料列數。 此選項可能大幅地增加效能。 例如，通常從一百萬個資料列中傳回 100,000 列的查詢，如果只要求前 100 個資料列的話，就會處理得更為快速。  
  
##  <a name="examples"></a> 使用 RANK 限制搜尋結果的範例  
  
### <a name="example-a-searching-for-only-the-top-three-matches"></a>範例 A：只搜尋前三個相符項目  
 下列範例會使用 CONTAINSTABLE，以便只傳回前三個相符項目。  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT K.RANK, AddressLine1, City  
FROM Person.Address AS A  
  INNER JOIN  
  CONTAINSTABLE(Person.Address, AddressLine1, 'ISABOUT ("des*",  
    Rue WEIGHT(0.5),  
    Bouchers WEIGHT(0.9))',  
    3) AS K  
  ON A.AddressID = K.[KEY]  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
RANK        Address                          City  
----------- -------------------------------- ------------------------------  
172         9005, rue des Bouchers           Paris  
172         5, rue des Bouchers              Orleans  
172         5, rue des Bouchers              Metz  
  
(3 row(s) affected)  
```  
  
  
### <a name="example-b-searching-for-the-top-ten-matches"></a>範例 B：搜尋前十個相符項目  
 下列範例會使用 CONTAINSTABLE 傳回 `Description` 資料行在 "light" 或 "lightweight" 字附近包含 "aluminum" 一字的前 5 項產品描述。  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT FT_TBL.ProductDescriptionID,  
   FT_TBL.Description,   
   KEY_TBL.RANK  
FROM Production.ProductDescription AS FT_TBL INNER JOIN  
   CONTAINSTABLE (Production.ProductDescription,  
      Description,   
      '(light NEAR aluminum) OR  
      (lightweight NEAR aluminum)',  
      5  
   ) AS KEY_TBL  
   ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
GO  
```  
  
  
##  <a name="how"></a> 搜尋查詢結果如何排序次序  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的全文檢索搜尋可以產生選擇性分數 (或次序值)，表示全文檢索查詢傳回之資料的相關性。 這個等級值是針對每個資料列計算的，而且可當做排序準則使用，以便依據相關性排序給定查詢的結果集。 等級值僅表示結果集中資料列相關性的相對順序。 實際的值並不重要，而且每次執行查詢後該值通常會不一樣。 次序值不會在查詢之間保存任何重要性。  
  
### <a name="statistics-for-ranking"></a>排序的統計資料  
 建立索引時會收集統計資料供評定等級使用。 建立全文檢索目錄的程序並不會直接導致單一索引結構。 相反地，Full-Text Engine for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在編製資料索引時建立中繼索引。 接著，全文檢索引擎會視需要將這些索引合併到較大的索引。 此程序可以重複許多次。 接著，全文檢索引擎會執行「主要合併」，將所有的中繼索引合併至較大的主索引。  
  
 統計資料是在每個中繼索引層級中收集。 合併索引時會合併統計資料。 某些統計資料值只能在主要合併程序期間產生。  
  
 計算查詢結果集的等級時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會使用最大中繼索引的統計資料。 需視中繼索引合併與否而定。 因此，如果中繼索引尚未合併，等級統計資料的精確度可能會有所變動。 這能解釋為何在一段時間的新增、修改、刪除全文檢索索引資料，以及在合併較小的索引之後，相同的查詢會傳回不同的等級結果。  
  
 為了降低索引大小與計算的複雜度，通常會將統計資料四捨五入。  
  
 下列清單包含一些計算等級時常用的重要詞彙與統計資料值。  
  
 屬性  
 資料列的全文檢索索引資料行。  
  
 Document  
 在查詢中傳回的實體。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，它會對應至資料列。 文件可以有多種屬性，就像資料列可以有多個全文檢索索引資料行。  
  
 索引  
 一或多個文件的單一反向索引。 它可能完全位於記憶體或磁碟中。 許多查詢統計資料會與符合項目的個別索引有關。  
  
 全文檢索目錄  
 被視為查詢的一個實體的中繼索引集合。 目錄為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理員可看見的組織單位。  
  
 單字、Token 或項目  
 全文檢索引擎中的比對單位。 會依語言特有的文字分隔，將文件中的文字資料流 Token 化為字組或 Token。  
  
 出現次數  
 文件屬性中的文字位移，此文字位移由文字分隔來決定。 第一個字是在發生 1，下個字是在發生 2，其餘依此類推。 為避免片語誤判與近似查詢，句子的結尾與段落結尾會加入較大的發生間距。  
  
 TermFrequency  
 資料列中出現的索引鍵值次數。  
  
 IndexedRowCount  
 已編製索引的資料列總數。 這會根據中繼索引中所維護的計數來計算。 此數字在精確度上會有所不同。  
  
 KeyRowCount  
 含有指定索引鍵之全文檢索目錄的資料列總數。  
  
 MaxOccurrence  
 全文檢索目錄中針對特定屬性儲存在資料列中的發生次數最大值。  
  
 MaxQueryRank  
 全文檢索引擎會傳回最大的等級是 1000。  
  
  
### <a name="rank-computation-issues"></a>等級計算問題  
 計算等級的程序取決於幾項因素。  不同語言的文字在分隔 Token 化文字的方式上會有所差異。 例如，使用某種文字分隔時會將 "dog-house" 字串分解成 "dog" "house"，而使用另一種文字分隔時會分解成 "dog-house"。 這表示比對和等級會依據指定的語言而異，因為不僅單字不同，而且文件長度也不同。 文件長度的差異會影響所有查詢的等級。  
  
 統計資料 (例如 **IndexRowCount** ) 可能會有很大的差異。 例如，如果某個目錄在主索引中有 20 億個資料列，則會將一個新文件的索引編製到記憶體的中繼索引。而該文件會根據記憶體索引中的文件數目所得的等級，與主索引的文件等級進行非對稱比較。 因此，建議您在執行任何會造成大量資料列編製索引或重新編製索引的母體擴展動作後，使用 ALTER FULLTEXT CATALOG ... REORGANIZE [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式來將這些索引與主要的索引合併。 全文檢索引擎也會根據參數 (例如中繼索引的數目與大小) 來自動合併索引。  
  
 **MaxOccurrence** 值會正規化為 32 種範圍中的其中一種。 這表示，會將長度 50 個字的文件視為與長度 100 個字的文件一樣。 下表用於正規化作業。 因為這兩個文件的長度在相鄰資料表值 32 到 128 的範圍內，因此它們會被視為具有相同長度的文件，也就是 128 (32 < **docLength** <= 128)。  
  
```  
{ 16, 32, 128, 256, 512, 725, 1024, 1450, 2048, 2896, 4096, 5792, 8192, 11585,   
16384, 23170, 28000, 32768, 39554, 46340, 55938, 65536, 92681, 131072, 185363,   
262144, 370727, 524288, 741455, 1048576, 2097152, 4194304 };  
  
```  
  
  
### <a name="ranking-of-containstable"></a>CONTAINSTABLE 的等級  
 [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) 等級會使用下列演算法：  
  
```  
StatisticalWeight = Log2( ( 2 + IndexedRowCount ) / KeyRowCount )  
Rank = min( MaxQueryRank, HitCount * 16 * StatisticalWeight / MaxOccurrence )  
```  
  
 片語比對會像個別索引鍵一樣來分級，但是會估計 **KeyRowCount** (含有片語的資料列數目)，而且該值可能不正確並高於實際數目。  
  
 **NEAR 的等級**  
  
 CONTAINSTABLE 支援使用 NEAR 選項來查詢彼此相近的兩個或多個搜尋詞彙。 每個傳回之資料列的等級值是以許多參數為基礎。 其中一個主要次序因數是相對於文件長度的符合項目 (或「叫用」) 總數。 因此，例如，如果 100 個字的文件和 900 個字的文件包含完全相同的符合項目，100 個字的文件就會具有較高的等級。  
  
 資料列中每個叫用的總長度也會根據該叫用之第一個和最後一個搜尋詞彙之間的距離影響該資料列的等級。 距離越小，叫用對資料列等級值造成的影響就越大。 如果全文檢索查詢沒有指定整數做為最大距離，只包含距離大於 100 個邏輯詞彙之叫用的文件將具有等級 0。  
  
 **ISABOUT 的等級**  
  
 CONTAINSTABLE 支援使用 ISABOUT 選項來查詢加權詞彙。 ISABOUT 是傳統資訊擷取詞彙中的向量空間查詢。 預設使用的等級演算法是 Jaccard，這是一個相當有名的公式。 會針對查詢中的每個詞彙計算等級，然後進行結合，如下表所述。  
  
```  
ContainsRank = same formula used for CONTAINSTABLE ranking of a single term (above).  
Weight = the weight specified in the query for each term. Default weight is 1.  
WeightedSum = Σ[key=1 to n] ContainsRankKey * WeightKey  
Rank =  ( MaxQueryRank * WeightedSum ) / ( ( Σ[key=1 to n] ContainsRankKey^2 )   
      + ( Σ[key=1 to n] WeightKey^2 ) - ( WeightedSum ) )  
  
```  
  
  
### <a name="ranking-of-freetexttable"></a>FREETEXTTABLE 的等級  
 [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) 等級是以 OKAPI BM25 等級公式為基礎。 FREETEXTTABLE 查詢會透過變化衍生項 (原始查詢字的變化型式) 將單字加入到查詢中。這些單字會視為個別單字，而且與來源產生字沒有特殊的關聯性。 由「同義字」功能所產生的同義字會視為個別詞彙，且加權值相同的詞彙。 查詢中的每個單字都是計算等級的基礎。  
  
```  
Rank = Σ[Terms in Query] w ( ( ( k1 + 1 ) tf ) / ( K + tf ) ) * ( ( k3 + 1 ) qtf / ( k3 + qtf ) ) )  
Where:   
w is the Robertson-Sparck Jones weight.   
In simplified form, w is defined as:   
w = log10 ( ( ( r + 0.5 ) * ( N - R + r + 0.5 ) ) / ( ( R - r + 0.5 ) * ( n - r + 0.5 ) )  
N is the number of indexed rows for the property being queried.   
n is the number of rows containing the word.   
K is ( k1 * ( ( 1 - b ) + ( b * dl / avdl ) ) ).   
dl is the property length, in word occurrences.   
avdl is the average length of the property being queried, in word occurrences.   
k1, b, and k3 are the constants 1.2, 0.75, and 8.0, respectively.   
tf is the frequency of the word in the queried property in a specific row.   
qtf is the frequency of the term in the query.   
```  
  
  
## <a name="see-also"></a>另請參閱  
 [使用全文檢索搜尋進行查詢](../../relational-databases/search/query-with-full-text-search.md)  
  
  
