---
title: 選擇性 XML 索引的路徑與最佳化提示 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
ms.assetid: 486ee339-165b-4aeb-b760-d2ba023d7d0a
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
ms.openlocfilehash: e4ffb1cc9a2b63047c6ade58d82001a2e0ebea4c
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/19/2019
ms.locfileid: "75257608"
---
# <a name="specify-paths-and-optimization-hints-for-selective-xml-indexes"></a>指定選擇性 XML 索引的路徑和最佳化提示
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  本主題描述如何指定建立或修改選擇性 XML 索引時，要索引的節點路徑以及索引的最佳化提示。  
  
 您會同時在下列其中一個陳述式中指定節點路徑及最佳化提示：  
  
-   在 **CREATE** 陳述式的 **FOR** 子句中。 如需詳細資訊，請參閱 [CREATE SELECTIVE XML INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-selective-xml-index-transact-sql.md)。  
  
-   在 **ALTER** 陳述式的 **ADD** 子句中。 如需詳細資訊，請參閱 [ALTER INDEX &#40;選擇性 XML 索引&#41;](../../t-sql/statements/alter-index-selective-xml-indexes.md)。  
  
 如需選擇性 XML 索引的詳細資訊，請參閱 [選擇性 XML 索引 &#40;SXI&#41;](../../relational-databases/xml/selective-xml-indexes-sxi.md)。  
  
##  <a name="untyped"></a> 了解不具類型之 XML 中的 XQuery 和 SQL Server 類型  
 選擇性 XML 索引支援兩種類型的系統：XQuery 類型和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 類型。 索引路徑可用來比對 XQuery 運算式，或是比對 XML 資料類型之 value() 方法的傳回類型。  
  
-   如果要索引的路徑未加上註解，或是使用 XQUERY 關鍵字註解，則路徑會比對 XQuery 運算式。 XQUERY 註解的節點路徑有兩種變化：  
  
    -   如果您未指定 XQUERY 關鍵字和 XQuery 資料類型，則會使用預設對應。 通常效能和儲存不是最佳的。  
  
    -   如果您指定 XQUERY 關鍵字和 XQuery 資料類型，並且選擇性地指定其他最佳化提示，就可以達到最佳效能和最有效率的儲存。 不過，轉換可能會失敗。  
  
-   如果要索引的路徑是以 SQL 關鍵字註解，則路徑符合 XML 資料類型之 value() 方法的傳回類型。 指定適當的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型，也就是預期從 value() 方法得到的傳回類型。  
  
 XQuery 運算式 XML 類型系統與套用至 XML 資料類型之 value() 方法的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 類型系統之間存在細微的差異。 這些差異包括下列幾項：  
  
-   XQuery 類型系統會考慮尾端空白。 例如，根據 XQuery 類型語意，字串 "abc" 與 "abc " 不相等，但在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中這些字串相等。  
  
-   XQuery 浮點資料類型支援 +/- 零和 +/- 無限大這些特殊值。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 浮點資料類型不支援這些特殊值。  
  
### <a name="xquery-types-in-untyped-xml"></a>不具類型 XML 中的 XQuery 類型  
  
-   XQuery 類型會比對 XML 資料類型之所有方法中的 XQuery 運算式，包含 value() 方法。  
  
-   XQuery 類型支援這些最佳化提示：node()、SINGLETON、DATA TYPE 和 MAXLENGTH。  
  
 對於在不具類型 XML 上的 XQuery 運算式，您可以選擇兩種作業模式：  
  
-   **預設對應模式**。 在此模式中，您只會指定建立選擇性 XML 索引時的路徑。  
  
-   **使用者指定的對應模式**。 在此模式中，您會指定路徑和選用的最佳化提示。  
  
 預設對應模式一律使用安全且普遍的保守儲存選項。 它可以比對任何運算式類型。 預設對應模式的限制比最佳效能少，因為需要執行階段轉換的次數增加，而且次要索引無法使用。  
  
 以下範例是使用預設對應建立的選擇性 XML 索引。 針對這三種路徑會使用預設節點類型 (**xs:untypedAtomic**) 和基數。  
  
```sql  
CREATE SELECTIVE XML INDEX example_sxi_UX_default  
ON Tbl(xmlcol)  
FOR  
(  
mypath01 =  '/a/b',  
mypath02 = '/a/b/c',  
mypath03 = '/a/b/d'  
)  
```  
  
 使用者指定的對應模式可讓您指定類型和基數，讓節點獲得更佳的效能。 不過，這種效能提升是藉由降低安全性 (因為轉換可能會失敗) 與普遍性 (因為只有指定的類型會與選擇性 XML 索引比對) 達成。  
  
 不具類型 XML 轉換所支援的 XQuery 類型包括：  
  
-   **xs:boolean**  
  
-   **xs:double**  
  
-   **xs:string**  
  
-   **xs:date**  
  
-   **xs:time**  
  
-   **xs:dateTime**  
  
 如果未指定類型，則會假設節點為 **xs:untypedAtomic** 資料類型。  
  
 您可以最佳化透過下列方式顯示的選擇性 XML 索引：  
  
```sql  
CREATE SELECTIVE XML INDEX example_sxi_UX_optimized  
ON Tbl(xmlcol)  
FOR  
(  
mypath= '/a/b' as XQUERY 'node()',  
pathX = '/a/b/c' as XQUERY 'xs:double' SINGLETON,  
pathY = '/a/b/d' as XQUERY 'xs:string' MAXLENGTH(200) SINGLETON  
)  
-- mypath - Only the node value is needed; storage is saved.  
-- pathX - Performance is improved; secondary indexes are possible.  
-- pathY - Performance is improved; secondary indexes are possible; storage is saved.  
```  
  
### <a name="sql-server-types-in-untyped-xml"></a>不具類型 XML 中的 SQL Server 類型  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 類型會比對 value() 方法的傳回值。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 類型支援此最佳化提示：SINGLETON。  
  
 對於傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 類型的路徑必須強制指定類型。 請使用您在 value() 方法中所使用的相同 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 類型。  
  
 請考慮以下查詢：  
  
```sql  
SELECT T.record,  
    T.xmldata.value('(/a/b/d)[1]', 'NVARCHAR(200)')  
FROM myXMLTable T  
```  
  
 指定的查詢會從封裝至 NVARCHAR(200) 資料類型內的路徑 `/a/b/d` 傳回值，因此要為節點指定的資料類型就很明顯。 不過，沒有用來在不具類型的 XML 中指定節點基數的結構描述。 若要指定節點 `d` 在其父節點 `b`下最多出現一次，請建立使用 SINGLETON 最佳化提示的選擇性 XML 索引，如下所示：  
  
```sql  
CREATE SELECTIVE XML INDEX example_sxi_US  
ON Tbl(xmlcol)  
FOR  
(  
node1223 = '/a/b/d' as SQL NVARCHAR(200) SINGLETON  
)  
```  
  
  
##  <a name="typed"></a> 了解具類型之 XML 的選擇性 XML 索引支援  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中具類型的 XML 是與特定 XML 文件相關聯的結構描述。 結構描述會定義節點的整體文件結構和類型。 如果結構描述存在，選擇性 XML 索引會在使用者升級路徑時套用結構描述結構，因此不需要指定路徑的 XQUERY 類型。  
  
 選擇性 XML 索引支援下列 XSD 類型：  
  
-   **xs:anyUri**  
  
-   **xs:boolean**  
  
-   **xs:date**  
  
-   **xs:dateTime**  
  
-   **xs:day**  
  
-   **xs:decimal**  
  
-   **xs:double**  
  
-   **xs:float**  
  
-   **xs:int**  
  
-   **xs:integer**  
  
-   **xs:language**  
  
-   **xs:long**  
  
-   **xs:name**  
  
-   **xs:NCName**  
  
-   **xs:negativeInteger**  
  
-   **xs:nmtoken**  
  
-   **xs:nonNegativeInteger**  
  
-   **xs:nonPositiveInteger**  
  
-   **xs:positiveInteger**  
  
-   **xs:qname**  
  
-   **xs:short**  
  
-   **xs:string**  
  
-   **xs:time**  
  
-   **xs:token**  
  
-   **xs:unsignedByte**  
  
-   **xs:unsignedInt**  
  
-   **xs:unsignedLong**  
  
-   **xs:unsignedShort**  
  
 在擁有相關結構描述的文件上建立選擇性 XML 索引時，於建立或修改索引時指定 XQUERY 會傳回錯誤。 使用者可以在路徑升級部分使用 SQL 類型註解。 SQL 類型必須是來自結構描述中所定義 XSD 類型的有效轉換，否則會擲回錯誤。 所有具有適當 XSD 表示的 SQL 類型都可支援，但不包括日期/時間類型。  
  
> [!NOTE]  
>  如果選擇性 XML 索引路徑升級中指定的類型與 value() 方法傳回值相同，則會使用選擇性索引。  
  
 下列最佳化提示可以搭配具類型的 XML 文件使用：  
  
-   node() 最佳化提示。  
  
-   MAXLENGTH 最佳化提示可以搭配 xs:string 類型用來縮短索引值。  
  
 如需最佳化提示的詳細資訊，請參閱 [指定最佳化提示](#hints)。  
  
##  <a name="paths"></a> 指定路徑  
 選擇性 XML 索引可讓您僅索引與預期執行之查詢相關的預存 XML 資料中節點的子集。 如果相關節點的子集大幅少於 XML 文件中節點的總數，選擇性 XML 索引只會儲存相關的節點。 若要利用選擇性 XML 索引的優點，請識別要索引的正確節點子集。  
  
### <a name="choosing-the-nodes-to-index"></a>選擇要索引的節點  
 您可以利用下列兩種簡單的原則，識別要加入至選擇性 XML 索引的正確節點子集。  
  
1.  **原則 1**：若要評估特定 XQuery 運算式，請為您需要檢查的所有節點編製索引。  
  
    -   索引在 XQuery 運算式中存在或使用其值的所有節點。  
  
    -   索引 XQuery 運算式中套用 XQuery 述詞的所有節點。  
  
     請考慮在本主題中 [範例 XML 文件](#sample) 上進行下列簡單的查詢：  
  
    ```sql  
    SELECT T.record FROM myXMLTable T  
    WHERE T.xmldata.exist('/a/b[./c = "43"]') = 1  
    ```  
  
     為了傳回滿足此查詢的 XML 執行個體，選擇性 XML 索引需要在每一個 XML 執行個體中檢查兩個節點：  
  
    -   節點 `c`，因為它的值在 XQuery 運算式中使用。  
  
    -   節點 `b`，因為述詞會在 XQuery 運算式的節點`b` 上套用。  
  
2.  **原則 2**：為了達到最佳效能，請為評估指定 XQuery 運算式所需的所有節點編製索引。 如果您只索引部分節點，則選擇性 XML 索引可改善僅包括索引節點的子運算式評估。  

 若要改善上面所示 SELECT 陳述式的效能，您可以建立下列選擇性 XML 索引：  
  
```sql  
CREATE SELECTIVE XML INDEX simple_sxi  
ON Tbl(xmlcol)  
FOR  
(  
    path123 =  '/a/b',  
    path124 =  '/a/b/c'  
)  
```  
  
### <a name="indexing-identical-paths"></a>索引相同路徑  
 您無法將相同路徑升級為路徑名稱不同的相同類型。 例如，下列查詢會引發錯誤，因為 `pathOne` 和 `pathTwo` 相同：  
  
```sql  
CREATE SELECTIVE INDEX test_simple_sxi ON T1(xmlCol)  
FOR  
(  
    pathOne = 'book/authors/authorID' AS XQUERY 'xs:string',  
    pathTwo = 'book/authors/authorID' AS XQUERY 'xs:string'  
)  
```  
  
 不過，您可以將相同路徑升級為具有不同名稱的不同資料類型。 例如，現在可接受下列查詢，因為資料類型不同：  
  
```sql  
CREATE SELECTIVE INDEX test_simple_sxi ON T1(xmlCol)  
FOR  
(  
    pathOne = 'book/authors/authorID' AS XQUERY 'xs:double',  
    pathTwo = 'book/authors/authorID' AS XQUERY 'xs:string'  
)  
```  
  
### <a name="examples"></a>範例  
 以下提供一些針對不同 XQuery 類型選取要索引之正確節點的其他範例。  
  
 **範例 1**  
  
 以下是使用 exist() 方法的簡單 XQuery：  
  
```sql  
SELECT T.record FROM myXMLTable T  
WHERE T.xmldata.exist('/a/b/c/d/e/h') = 1  
```  
  
 下表顯示應索引的節點，以便讓這個查詢使用選擇性 XML 索引。  
  
|要包含在索引中的節點|索引此節點的原因|  
|----------------------------------|-----------------------------------|  
|**/a/b/c/d/e/h**|會在 exist() 方法中評估節點 `h` 是否存在。|  
  
 **範例 2**  
  
 以下是前一個 XQuery 較為複雜的變化，其中會套用述詞：  
  
```sql  
SELECT T.record FROM myXMLTable T  
WHERE T.xmldata.exist('/a/b/c/d/e[./f = "SQL"]') = 1  
```  
  
 下表顯示應索引的節點，以便讓這個查詢使用選擇性 XML 索引。  
  
|要包含在索引中的節點|索引此節點的原因|  
|----------------------------------|-----------------------------------|  
|**/a/b/c/d/e**|述詞會套用在節點 `e`上。|  
|**/a/b/c/d/e/f**|節點 `f` 的值會在述詞內評估。|  
  
 **範例 3**  
  
 以下查詢較為複雜，會使用 value() 子句：  
  
```sql  
SELECT T.record,  
    T.xmldata.value('(/a/b/c/d/e[./f = "SQL"]/g)[1]', 'nvarchar(100)')  
FROM myXMLTable T  
```  
  
 下表顯示應索引的節點，以便讓這個查詢使用選擇性 XML 索引。  
  
|要包含在索引中的節點|索引此節點的原因|  
|----------------------------------|-----------------------------------|  
|**/a/b/c/d/e**|述詞會套用在節點 `e`上。|  
|**/a/b/c/d/e/f**|節點 `f` 的值會在述詞內評估。|  
|**/a/b/c/d/e/g**|節點 `g` 的值是由 value() 方法傳回。|  
  
 **範例 4**  
  
 以下是在 exist() 子句內使用 FLWOR 子句的查詢 (FLWOR 這個名稱來自五個子句，這五個子句構成 XQuery FLWOR 運算式：for、let、where、order by 和 return)。  
  
```sql  
SELECT T.record FROM myXMLTable T  
WHERE T.xmldata.exist('  
  For $x in /a/b/c/d/e  
  Where $x/f = "SQL"  
  Return $x/g  
') = 1  
```  
  
 下表顯示應索引的節點，以便讓這個查詢使用選擇性 XML 索引。  
  
|要包含在索引中的節點|索引此節點的原因|  
|----------------------------------|-----------------------------------|  
|**/a/b/c/d/e**|FLWOR 子句中會評估節點 `e` 是否存在。|  
|**/a/b/c/d/e/f**|節點 `f` 的值會在 FLWOR 子句中評估。|  
|**/a/b/c/d/e/g**|exist() 方法會評估節點 `g` 是否存在。|  
  
  
##  <a name="hints"></a> 指定最佳化提示  
 您可以使用選用的最佳化提示，為藉由選擇性 XML 索引進行索引的節點指定其他對應詳細資料。 例如，您可以指定節點的資料類型和基數，以及有關資料結構的特定資訊。 這項額外資訊可提供更佳的對應。 此外還能獲得效能提升和 (或) 節省儲存空間的結果。  
  
 最佳化提示是選擇性的用法。 您可以一律接受預設對應，預設對應雖然可靠，但不一定能提供最佳效能和儲存。  
  
 某些最佳化提示 (例如，SINGLETON 提示) 會對資料形成條件約束。 在某些情況下，如果不符合這些條件約束，可能會引發錯誤。  
  
### <a name="benefits-of-optimization-hints"></a>最佳化提示的優點  
 下表會識別支援更有效率的儲存或提升效能的最佳化提示。  
  
|最佳化提示|更有效率的儲存|提升效能|  
|-----------------------|----------------------------|--------------------------|  
|**node()**|是|否|  
|**SINGLETON**|否|是|  
|**DATA TYPE**|是|是|  
|**MAXLENGTH**|是|是|  
  
### <a name="optimization-hints-and-data-types"></a>最佳化提示和資料類型  
 您可以索引 XQuery 資料類型或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型的節點。 下表顯示每一種資料類型支援的最佳化提示。  
  
|最佳化提示|XQuery 資料類型|SQL 資料類型|  
|-----------------------|-----------------------|--------------------|  
|**node()**|是|否|  
|**SINGLETON**|是|是|  
|**DATA TYPE**|是|否|  
|**MAXLENGTH**|是|否|  
  
### <a name="node-optimization-hint"></a>node() 最佳化提示  
 適用於：XQuery 資料類型  
  
 您可以使用 node() 最佳化指定評估一般查詢時不需要其值的節點。 這個提示可在一般查詢只需評估節點是否存在時，減少儲存需求 (根據預設，選擇性 XML 索引會儲存所有已升級節點的值，但是不包括複雜的節點類型)。  
  
 請考慮下列範例：  
  
```sql  
SELECT T.record FROM myXMLTable T  
WHERE T.xmldata.exist('/a/b[./c=5]') = 1  
```  
  
 若要使用選擇性 XML 索引評估此查詢，請升級節點 `b` 和 `c`。 不過，由於不需要節點 `b` 的值，因此您可以使用下列語法的 node() 提示：  
  
 `/a/b/ as node()`  
  
 如果查詢需要已利用 node() 提示索引之節點的值，則無法使用選擇性 XML 索引。  
  
### <a name="singleton-optimization-hint"></a>SINGLETON 最佳化提示  
 適用於：XQuery 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型  
  
 SINGLETON 最佳化提示會指定節點的基數。 此提示可改善查詢效能，因為事先就已知道節點最多只會在其父系或上階內出現一次。  
  
 請考慮本主題中的 [範例 XML 文件](#sample) 。  
  
 若要使用選擇性 XML 索引查詢此文件，您可以針對節點 `d` 指定 SINGLETON 提示，因為它最多只會在其父系內出現一次。  
  
 如果已指定 SINGLETON 提示，但節點在其父系或上階內不只出現一次，則會在您建立索引 (針對現有資料) 或執行查詢 (針對新資料) 時引發錯誤。  
  
### <a name="data-type-optimization-hint"></a>DATA TYPE 最佳化提示  
 適用於：XQuery 資料類型  
  
 DATA TYPE 最佳化提示可讓您針對索引的節點指定 XQuery 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型。 資料類型用於對應索引節點的選擇性 XML 索引之資料表中的資料行。  
  
 將現有值轉換成指定的資料類型失敗時，插入作業 (插入索引內) 不會失敗；但是索引的資料表中會插入 null 值。  
  
### <a name="maxlength-optimization-hint"></a>MAXLENGTH 最佳化提示  
 適用於：XQuery 資料類型  
  
 MAXLENGTH 最佳化提示可讓您限制 xs:string 資料的長度。 MAXLENGTH 與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型無關，因為您是在指定 VARCHAR 或 NVARCHAR 資料類型時指定長度。  
  
 如果現有的字串長度超過指定的 MAXLENGTH，則將該值插入索引中的作業會失敗。  
  
  
##  <a name="sample"></a> 做為範例的範例 XML 文件  
 下列範例 XML 文件會在本主題的範例中參考：  
  
```xml  
<a>  
    <b>  
         <c atc="aa">10</c>  
         <c atc="bb">15</c>  
         <d atd1="dd" atd2="ddd">md </d>  
    </b>  
     <b>  
        <c></c>  
        <c atc="">117</c>  
     </b>  
</a>  
```  
  
  
## <a name="see-also"></a>另請參閱  
 [選擇性 XML 索引 &#40;SXI&#41;](../../relational-databases/xml/selective-xml-indexes-sxi.md)   
 [建立、修改和卸除選擇性 XML 索引](../../relational-databases/xml/create-alter-and-drop-selective-xml-indexes.md)  
  
  
