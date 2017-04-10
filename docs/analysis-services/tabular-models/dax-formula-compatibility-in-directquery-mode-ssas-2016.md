---
title: "DirectQuery 模式中的 DAX 公式相容性 (SSAS 2016) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d2fbafe6-d7fb-437b-b32b-fa2446023fa5
caps.latest.revision: 10
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 10
---
# DirectQuery 模式中的 DAX 公式相容性 (SSAS 2016)
[!INCLUDE[ssASCurrent_md](../../includes/ssascurrent-md.md)] 中部分最重要的增強功能為表格式 1200 模型的 DirectQuery 模式功能。 在舊版中的許多功能限制不再適用。 特別針對 DAX 公式︰

- DirectQuery 現在會產生較簡單的查詢，提供更佳的效能。
- DirectQuery 模式中的表格式 1200 模型現在支援資料列層級安全性 (RLS)。
- DirectQuery 模式中的表格式 1200 模型現在支援導出資料行。

## DirectQuery 模式中的 DAX 函數

簡單地說，表格式 1200 DirectQuery 模型支援所有 DAX 函數。 不過，並非所有函數都支援所有公式類型，而且並非所有函數都已針對表格式 1200 DirectQuery 模型最佳化。 在最基本的層級，我們可以將 DAX 函數分為兩大派︰最佳化與非最佳化。 首先讓我們仔細看看最佳化的函數。


### 針對 DirectQuery 最佳化
這些是主要會傳回純量或彙總結果的功能。 這些函數可進一步細分為在所有類型公式中支援的項目︰量值、查詢、導出資料行、資料列層級安全性，以及僅在量值和查詢公式中支援的項目。 其中包括：    

| 支援所有 DAX 公式                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | 僅支援量值和查詢公式                                                                                                                                                                                                                                                                                                |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ABS</br>  ACOS</br>  ACOT</br>  與</br>  ASIN</br>  ATAN</br>  BLANK</br>  CEILING</br>  CONCATENATE</br>  COS</br>  COT</br>  CURRENCY</br>  DATE</br>  DATEDIFF</br>  DATEVALUE</br>  DAY</br>  DEGREES</br>  DIVIDE</br>  EDATE</br>  EOMONTH</br>  EXACT</br>  EXP</br>  FALSE</br>  FIND</br>  HOUR</br>  IF</br>  INT</br>  ISBLANK</br>  ISO.CEILING</br>  KEEPFILTERS</br>  LEFT</br>  LEN</br>  LN</br>  LOG</br>  LOG10</br>  LOWER</br>  MAX</br>  MID</br>  MIN</br>  MINUTE</br>  MOD</br>  MONTH</br>  MROUND</br>  NOT</br>  NOW</br>  OR</br>  PI</br>  POWER</br>  QUOTIENT</br>  RADIANS</br>  RAND</br>  RELATED</br>  REPT</br>  RIGHT</br>  ROUND</br>  ROUNDDOWN</br>  ROUNDUP</br>  SEARCH</br>  SECOND</br>  SIGN</br>  SIN</br>  SQRT</br>  SQRTPI</br>  SUBSTITUTE</br>  SWITCH</br>  TAN</br>  TIME</br>  TIMEVALUE</br>  TODAY</br>  TRIM</br>  TRUE</br>  TRUNC</br>  UNICODE</br>  UPPER</br>  USERNAME</br>  USERELATIONSHIP</br>  值</br>  WEEKDAY</br>  WEEKNUM</br>  YEAR</br> | ALL</br> ALLEXCEPT</br> ALLNOBLANKROW</br> ALLSELECTED</br> AVERAGE</br> AVERAGEA</br> AVERAGEX</br> CALCULATE</br> CALCULATETABLE</br> COUNT</br> COUNTA</br> COUNTAX</br> COUNTROWS</br> COUNTX</br> DISTINCT</br> DISTINCTCOUNT</br> FILTER</br> FILTERS</br> HASONEFILTER</br> HASONEVALUE</br> ISCROSSFILTERED</br> ISFILTERED</br> MAXA</br> MAXX</br> MIN</br> MINA</br> MINX</br> RELATEDTABLE</br> STDEV.P</br> STDEV.S</br> STDEVX.P</br> STDEVX.S</br> SUM</br> SUMX</br> VALUES</br> VAR.P</br> VAR.S</br> VARX.P</br> VARX.S |



### 未針對 DirectQuery 最佳化
這些函數尚未最佳化，以在表格式 1200 模型中使用 DirectQuery。 導出資料行和資料列層級安全性公式完全「不」支援這些函數。 不過， 量值和查詢公式「支援」這些函數，隨然效能並不確定。

 我們不會在此列出所有的函數。 基本上，如果不是上述列出的其中一種最佳化函數，它就不是針對 DirectQuery 的最佳化功能。

特定函數可能未針對 DirectQuery 最佳化的原因，是因為基礎關聯式引擎無法執行相當於 xVelocity 引擎所執行的計算，或公式無法轉換為相等的 SQL 運算式。 在其他情況下，轉換運算式以及產生的計算效能可能令人無法接受。

若要深入了解所有 DAX 函數，請參閱 [DAX 函數參考]。(https://msdn.microsoft.com/en-us/library/ee634396.aspx)

## 在 DirectQuery 模式中的 DAX 運算子
在 DirectQuery 模式的表格式 1200 模型中完全支援所有 DAX 比較和算術運算子。 若要深入了解，請參閱 [DAX 運算子參考](https://msdn.microsoft.com/library/ee634237.aspx)。


 
## 記憶體內部與 DirectQuery 模式之間的差異  
在 DirectQuery 模式中部署之模型的查詢，可能會傳回與在記憶體內部模式中部署之相同模型的不同結果。 這是 DirectQuery 所導致的，資料直接從關聯式資料存放區查詢，並使用相關的關聯式引擎 (SQL、Oracle、Teradata) 執行公式所需的彙總，而不使用 xVelocity 記憶體內部分析引擎來進行儲存和計算。  
  
例如，某些關聯式資料存放區處理數值、日期、Null 等項目的方式就有差異。  
  
相較之下，DAX 語言的目的是要盡可能模擬 Microsoft Excel 中函數的行為。 例如，在處理 Null、空字串和零值時，Excel 會嘗試提供最佳答案，而不考慮精確的資料類型，因此 xVelocity 引擎會執行相同的處理方式。 不過，當表格式模型以 DirectQuery 模式部署並且將公式傳遞給關聯式資料來源時，系統就必須根據關聯式資料來源的語意處理資料，而這通常需要以不同的方式處理空字串與 Null。 因此，根據快取的資料以及完全從關聯式存放區中傳回的資料進行評估時，相同的公式可能會傳回不同的結果。  
  
此外，某些函數沒有針對 DirectQuery 模式最佳化，因為計算會要求系統將目前內容中的資料當作參數傳送至關聯式資料來源。 比方說，測量使用參考行事曆資料表中日期範圍的時間智慧函數。 關聯式資料來源可能沒有行事曆資料表，或至少一個具有行事曆資料表。  
  
## 語意差異  
本節將列出您可以預期的語意差異類型，並且描述可能適用於函數使用方式或查詢結果的任何限制。  
  
### 比較  
記憶體內部模型中的 DAX 支援比較兩個解析為不同資料類型之純量值的運算式。 不過，在 DirectQuery 模式中部署的模型會使用關聯式引擎的資料類型和比較運算子，因此可能會傳回不同的結果。  
  
在 DirectQuery 資料來源的計算中使用時，下列比較一定會傳回錯誤：  
  
-   將數值資料類型與任何字串資料類型相比較  
  
-   將數值資料類型與布林值相比較  
  
-   將任何字串資料類型與布林值相比較  
  
一般而言，DAX 比較能夠容許記憶體內部模型的資料類型不符，而且將嘗試針對值進行隱含轉換 (最多兩次)，如本節所述。 不過，在 DirectQuery 模式中，傳送至關聯式資料存放區的公式會依照關聯式引擎的規則，以較嚴格的方式進行評估，而且比較可能會失敗。  
  
**字串和數字的比較**  
範例： `“2” < 3`  
  
此公式會比較文字字串與數字。 在 DirectQuery 模式和記憶體內部模型中，此運算式都是 **true**。  
  
在記憶體內部模型中，結果為 **true**，因為作為字串的數字會隱含轉換成數值資料類型，以便與其他數字進行比較。 SQL 也會將文字數字隱含轉換成數字，以便與數值資料類型相比較。  
  
請注意，這代表 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 第一版行為的變更 (原本傳回 **false**)，因為文字 “2” 一定會被視為大於任何數字。  
  
**文字與布林值的比較**  
範例： `“VERDADERO” = TRUE`  
  
此運算式會比較文字字串與布林值。 通常，對於 DirectQuery 或記憶體中模型而言，將字串值與布林值相比較會產生錯誤。 此規則的唯一例外狀況是，當字串包含 **true** 或 **false** 一字時。如果字串包含任何 true 或 false 值，就會轉換成布林值並且進行比較，並提供邏輯結果。  
  
**Null 的比較**  
範例： `EVALUATE ROW("X", BLANK() = BLANK())`  
  
此公式會比較兩個 Null 是否為 SQL 對等項目。 在記憶體內部模型和 DirectQuery 模型中，它會傳回 **true**。DirectQuery 模型會進行佈建，確保記憶體內部模型具有相似的行為。  
  
請注意，在 Transact-SQL 中，Null 永遠不等於 Null。 不過，在 DAX 中，某個空白會等於另一個空白。 這種行為對於所有記憶體中模型都相同。 請務必注意，DirectQuery 模式會使用 SQL Server 的大部分語意。不過，在此情況下，它會針對 NULL 比較提供新的行為，藉以區別。  
  
### 轉換  
  
雖然 DAX 沒有這類轉換函數，不過在許多比較和算術運算中，它會執行隱含轉換。 這就是決定結果資料類型的比較或算術運算。 例如，  
  
-   在算術運算中，布林值會被視為數值 (例如 TRUE + 1) 或是套用至布林值資料行的 MIN 函數。 NOT 運算也會傳回數值。  
  
-   進行比較而且搭配 EXACT、AND、OR、&amp;&amp; 或 || 使用時，布林值一定會被視為邏輯值。  
  
**從字串轉換成布林值**  
在記憶體內部模型和 DirectQuery 模型中，系統僅允許從這些字串轉換成布林值：**“”** (空字串)、**“true”**、**“false”**，其中空字串會轉換成 false 值。  
  
轉換成任何其他字串的布林資料類型會產生錯誤。  
  
**從字串轉換成日期/時間**  
在 DirectQuery 模式中，從日期和時間的字串表示轉換成實際的 **datetime** 值時，其行為方式與 SQL Server 相同。   
  
使用記憶體中資料存放區之模型所支援的日期文字格式範圍比 SQL Server 所支援的日期字串格式更有限。 不過，DAX 支援自訂日期和時間格式。  
  
**從字串轉換成其他非布林值**  
從字串轉換成非布林值時，DirectQuery 模式的行為與 SQL Server 相同。 如需詳細資訊，請參閱 [CAST 和 CONVERT (Transact-SQL)](http://msdn.microsoft.com/zh-tw/a87d0850-c670-4720-9ad5-6f5a22343ea8)。  
  
**不允許從數字轉換成字串**  
範例： `CONCATENATE(102,”,345”)`  
  
SQL Server 不允許從數字轉換成字串。  
  
在表格式模型和 DirectQuery 模式中，此公式會傳回錯誤。不過，在 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 中，此公式會產生結果。  
  
**在 DirectQuery 中不支援兩次嘗試轉換**  
當第一次轉換失敗時，記憶體中模型通常會嘗試第二次轉換。 這在 DirectQuery 模式中絕對不會發生。  
  
範例： `TODAY() + “13:14:15”`  
  
在此運算式中，第一個參數的類型為 **datetime**，而第二個參數的類型為 **string**。 不過，結合運算元時，系統將以不同的方式處理轉換。 DAX 將執行從 **string** 到 **double** 的隱含轉換。 在記憶體內部模型中，公式引擎會嘗試直接轉換成 **double**，而且如果轉換失敗，它會嘗試將字串轉換成 **datetime**。  
  
在 DirectQuery 模式中，系統只會套用從 **string** 到 **double** 的直接轉換。 如果這項轉換失敗，公式將傳回錯誤。  
  
### 數學函數和算術運算  
在 DirectQuery 模式中，某些數學函數會由於可在運算中套用之基礎資料類型或轉換的差異而傳回不同的結果。 此外，上述有關允許值範圍的限制可能也會影響算術運算的結果。  
  
**加法順序**  
當您建立將一連串數字相加的公式時，記憶體中模型處理這些數字的順序可能與 DirectQuery 模型不同。  因此，當您設有許多非常龐大的正數和負數時，可能會在某個運算中收到錯誤，而在另一個運算中取得結果。  
  
**POWER 函數的用法**  
範例： `POWER(-64, 1/3)`  
  
在 DirectQuery 模式中，當 POWER 函數提升為分數指數時，無法使用負值做為底數。 這是 SQL Server 的預期行為。  
  
在記憶體中模型中，此公式會傳回 -4。  
  
**數值溢位運算**  
在 Transact-SQL 中，產生數值溢位的運算會傳回溢位錯誤。因此，產生溢位的公式也會在 DirectQuery 模式中引發錯誤。  
  
不過，在記憶體中模型中使用相同的公式時，則會傳回八位元組整數。 這是因為公式引擎不會執行數值溢位的檢查。  
  
**含有空白的 LOG 函數會傳回不同的結果**  
SQL Server 處理 Null 和空白的方式與 xVelocity 引擎不同。 因此，下列公式會在 DirectQuery 模式中傳回錯誤，而在記憶體內部模式中傳回無限大 (–inf)。  
  
`EXAMPLE: LOG(blank())`  
  
相同的限制也適用於其他對數函數：LOG10 和 LN。  
  
如需 DAX 中 **blank** 資料類型的詳細資訊，請參閱 [DAX 語法參考](https://msdn.microsoft.com/library/ee634217.aspx)。  
  
**除以 0 和除以空白**  
在 DirectQuery 模式中，除以零 (0) 或除以 BLANK 都一定會產生錯誤。 SQL Server 不支援無限大的概念，而且因為任何除以 0 的自然結果都是無限大，所以結果就是錯誤。 不過，SQL Server 支援除以 Null，而且結果一定等於 Null。  
  
在 DirectQuery 模式中，這兩種運算類型 (除以零和除以 Null) 都會傳回錯誤，而非傳回不同的結果。  
  
請注意，在 Excel 和 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 模型中，除以零也會傳回錯誤。 除以空白則傳回空白。  
  
下列運算式在記憶體中模型中全部有效，但是在 DirectQuery 模式中則會失敗：  
  
`1/BLANK`  
  
`1/0`  
  
`0.0/BLANK`  
  
`0/0`  
  
運算式 `BLANK/BLANK` 是特殊案例，它會針對記憶體中模型和 DirectQuery 模式傳回 `BLANK`。  
  
### 支援的數值和日期-時間範圍  
就實數和日期的最大允許值而言，記憶體內部表格式模型中的公式受限於與 Excel 相同的限制。 不過，當最大值是從計算或查詢傳回，或者系統轉換、轉型、四捨五入或截斷值時，可能會發生差異。  
  
-   如果 **Currency** 和 **Real** 類型的值相乘，而且結果大於最大可能值，則在 DirectQuery 模式中，不會引發錯誤，而且會傳回 Null。  
  
-   在記憶體中模型中，不會引發錯誤，但是會傳回最大值。  
  
一般而言，因為 Excel 和 SQL Server 所接受的日期範圍不同，所以只有當日期位於共通日期範圍 (包括下列日期) 內時，才能保證結果相符：  
  
-   最早日期：1990 年 3 月 1 日  
  
-   最晚日期：9999 年 12 月 31 日  
  
如果公式中使用的任何日期超過這個範圍，則公式會產生錯誤，或者結果不符。  
  
**CEILING 支援的浮點值**  
範例： `EVALUATE ROW("x", CEILING(-4.398488E+30, 1))`  
  
DAX CEILING 函數的 Transact-SQL 對等項目僅支援大小為 10^19 以下的值。 基本原則是，浮點值應該能夠納入 **bigint** 中。  
  
**所含日期超出範圍的 Datepart 函數**  
只有當做為引數使用的日期位於有效的日期範圍內時，才能保證 DirectQuery 模式的結果與記憶體中模型的結果相符。 如果沒有滿足這些條件，則會引發錯誤，或者公式會在 DirectQuery 與記憶體中模式中傳回不同的結果。  
  
範例：`MONTH(0)` 或 `YEAR(0)`  
  
在 DirectQuery 模式中，這些運算式會分別傳回 12 和 1899。  
  
在記憶體中模型中，這些運算式會分別傳回 1 和 1900。  
  
範例：  `EOMONTH(0.0001, 1)`  
  
只有當提供做為參數的日期位於有效的日期範圍內時，此運算式的結果才會相符。  
  
範例：`EOMONTH(blank(), blank())` 或 `EDATE(blank(), blank())`  
  
在 DirectQuery 模式和記憶體中模式中，此運算式的結果應該都相同。  
  
**截斷時間值**  
範例： `SECOND(1231.04097222222)`  
  
在 DirectQuery 模式中，系統會依照 SQL Server 的規則截斷結果，而且此運算式會評估為 59。  
  
在記憶體中模型中，每個暫時運算的結果都會四捨五入。因此，運算式會評估為 0。  
  
下列範例將示範如何計算此值：  
  
1.  輸入的小數部分 (0.04097222222) 乘以 24。  
  
2.  產生的小時值 (0.98333333328) 乘以 60。  
  
3.  產生的分鐘值為 58.9999999968。  
  
4.  分鐘值的小數部分 (0.9999999968) 乘以 60。  
  
5.  產生的秒鐘值 (59.999999808) 四捨五入成 60。  
  
6.  60 等於 0。  
  
**不支援 SQL Time 資料類型**  
記憶體內部模型不支援使用新的 SQL **Time** 資料類型。 在 DirectQuery 模式中，參考含有此資料類型之資料行的公式會傳回錯誤。 時間資料行無法匯入記憶體中模型。  
  
不過，有時候引擎會將時間值轉換成可接受的資料類型，而且公式會傳回結果。  
  
這種行為會影響將日期資料行當做參數使用的所有函數。  
  
### <a name="bkmk_Currency"></a>貨幣  
在 DirectQuery 模式中，如果算術運算的結果為 **Currency** 類型，此值就必須位於下列範圍內：  
  
-   最小值：-922337203685477.5808  
  
-   最大值：922337203685477.5807  
  
**結合 Currency 與 REAL 資料類型**  
範例： `Currency sample 1`  
  
如果 **Currency** 和 **Real** 類型相乘，結果大於 9223372036854774784 (0x7ffffffffffffc00)，DirectQuery 模式不會引發錯誤。  
  
在記憶體內部模型中，如果結果的絕對值大於 922337203685477.4784，則會引發錯誤。  
  
**運算產生超出範圍的值**  
範例： `Currency sample 2`  
  
如果任兩個貨幣值的運算產生了超過指定範圍的值，記憶體中模型就會引發錯誤，但是 DirectQuery 模型不會引發錯誤。  
  
**結合 Currency 與其他資料類型**  
將貨幣值除以其他數值類型的值可能會產生不同的結果。  
  
### <a name="bkmk_Aggregations"></a>彙總函數  
含有一個資料列之資料表的統計函數會傳回不同的結果。 此外，空白資料表的彙總函式在記憶體中模型中表現的行為也與 DirectQuery 模式不同。  
  
**含有單一資料列之資料表的統計函數**  
如果當作引數使用的資料表包含單一資料列，在 DirectQuery 模式中，STDEV 和 VARx 等統計函數會傳回 Null。  
  
在記憶體內部模型中，針對含有單一資料列之資料表使用 STDEV 或 VARx 的公式會傳回除以零錯誤。  
  
### <a name="bkmk_Text"></a>文字函數  
因為關聯式資料存放區所提供的文字資料類型與 Excel 不同，所以當您搜尋字串或使用子字串時，可能會看見不同的結果。 字串的長度可能也不同。  
  
一般而言，任何使用固定大小資料行做為引數的字串操作函數都可能具有不同的結果。  
  
此外，在 SQL Server 中，某些文字函數支援 Excel 並未提供的其他引數。 如果公式需要遺漏的引數，您可能會在記憶體中模型中取得不同的結果或錯誤。  
  
**使用 LEFT、RIGHT 等函數傳回字元的運算可能會傳回正確但大小寫不同的字元，或者不傳回任何結果**  
範例： `LEFT([“text”], 2)`  
  
在 DirectQuery 模式中，傳回之字元的大小寫一定與儲存在資料庫中的字母完全相同。 不過，xVelocity 引擎會使用不同的演算法來壓縮值並建立索引，以便改善效能。  
  
根據預設，系統會使用 Latin1_General 定序，這種定序不區分大小寫，但是區分腔調字。 因此，如果某個文字字串具有多個採用小寫、大寫或混合大小寫的執行個體，所有執行個體都會被視為相同的字串，而且只有字串的第一個執行個體會儲存在索引中。 針對預存字串運作的所有文字函數都會擷取索引格式的指定部分。 因此，範例公式會使用第一個執行個體做為輸入，針對整個資料行傳回相同的值。  
  
這種行為也適用於其他文字函數，包括 RIGHT、MID 等等。  
  
**字串長度會影響結果**  
範例： `SEARCH(“within string”, “sample target  text”, 1, 1)`  
  
如果您使用 SEARCH 函數來搜尋字串，而且目標字串的長度超過 within string，DirectQuery 模式就會引發錯誤。  
  
在記憶體內部模型中，系統會傳回搜尋的字串，但是其長度會截斷至 &lt;within text&gt; 的長度。  
  
範例： `EVALUATE ROW("X", REPLACE("CA", 3, 2, "California") )`  
  
如果取代字串的長度大於原始字串的長度，在 DirectQuery 模式中，此公式會傳回 Null。  
  
在記憶體中模型中，此公式會依照 Excel 的行為 (串連來源字串與取代字串)，並且傳回 CACalifornia。  
  
**字串中間的隱含 TRIM**  
範例： `TRIM(“ A sample sentence with leading white space”)`  
  
DirectQuery 模式會將 DAX TRIM 函數轉譯成 SQL 陳述式 `LTRIM(RTRIM(<column>))`。 因此，只會移除開頭和尾端空白字元。  
  
相較之下，記憶體中模型中的相同公式會依照 Excel 的行為，移除字串內的空格。  
  
**搭配 LEN 函數使用的隱含 RTRIM**  
範例： `LEN(‘string_column’)`  
  
與 SQL Server 相同的是，DirectQuery 模式會自動從字串資料行的結尾移除空白字元：也就是說，它會執行隱含 RTRIM。 因此，如果字串具有尾端空格，使用 LEN 函數的公式可能會傳回不同的結果。  
  
**記憶體支援 SUBSTITUTE 的其他參數**  
範例： `SUBSTITUTE([Title],”Doctor”,”Dr.”)`  
  
範例： `SUBSTITUTE([Title],”Doctor”,”Dr.”, 2)`  
  
在 DirectQuery 模式中，您只能使用這個具有三個 (3) 參數的函數版本：資料行的參考、舊文字和新文字。 如果您使用第二個公式，就會引發錯誤。  
  
在記憶體中模型中，您可以使用選擇性的第四個參數來指定要取代之字串的執行個體編號。 例如，您可以單獨取代第二個執行個體。  
  
**REPT 運算的字串長度限制**  
在記憶體中模型中，使用 REPT 之運算所產生的字串長度必須小於 32,767 個字元。  
  
這項限制不適用於 DirectQuery 模式。  
  
**子字串運算會根據字元類型傳回不同的結果**  
範例： `MID([col], 2, 5)`  
  
如果輸入文字為 **varchar** 或 **nvarchar**，公式的結果一定相同。  
  
不過，如果文字是固定長度字元，而且 *&lt;num_chars&gt;* 的值大於目標字串的長度，在 DirectQuery 模式中，系統會在結果字串的結尾加入空白。  
  
在記憶體中模型中，結果會在最後一個字串字元處終止，而且沒有填補。  


## 另請參閱  
[DirectQuery 模式 (SSAS 表格式)](http://msdn.microsoft.com/zh-tw/45ad2965-05ec-4fb1-a164-d8060b562ea5)  
  


