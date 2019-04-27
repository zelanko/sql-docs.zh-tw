---
title: Cube 空間 |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 58f1a22cbba10eff6c10d2fc70dffcb13632b15d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62800202"
---
# <a name="cube-space"></a>Cube 空間
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  「Cube 空間」是 Cube 屬性階層中具有 Cube 量值之成員的乘積。 因此，Cube 空間是由 Cube 所有屬性階層成員和 Cube 量值的組合乘積所決定，定義了 Cube 的大小上限。 請務必注意，此空間包含屬性階層成員的所有可能組合，甚至還包含在真實世界中被視為不可能的組合，例如城市為巴黎而國家/地區為英國、西班牙、日本、印度或其他地方的組合。  
  
## <a name="autoexists-and-cube-space"></a>自動存在和 Cube 空間  
 「自動存在」的概念將此 Cube 空間限制於實際存在的資料格。 維度中屬性階層的成員可能不與相同維度中另一個屬性階層的成員同時存在。  
  
 例如，如果 Cube 有 City 屬性階層、Country 屬性階層及 Internet Sales Amount 量值，此 Cube 的空間只會包含同時存在的成員。 例如，如果 City 屬性階層包含紐約、倫敦、巴黎、東京及墨爾本等城市，並且 Country 屬性階層包含美國、英國、法國、日本及澳洲等國家 (地區)，則 Cube 的空間不會包含巴黎和美國交集的空間 (資料格)。  
  
 當查詢不存在的資料格時，不存在的資料格會傳回 Null，也就是說，它們不包含計算，而且您無法定義寫入此空間的計算。 例如，下列陳述式包括了不存在的資料格。  
  
```  
SELECT [Customer].[Gender].[Gender].Members ON COLUMNS,  
{[Customer].[Customer].[Aaron A. Allen]  
   ,[Customer].[Customer].[Abigail Clark]} ON ROWS   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
> [!NOTE]  
>  這個查詢使用 [Members (Set) (MDX)](../../../mdx/members-set-mdx.md) 函數來傳回資料行軸上 Gender 屬性階層的成員集合，並且將該集合與資料列軸上 Customer 屬性階層的指定成員集合相交。  
  
 當您執行上述查詢時，Aaron A. Allen 和 Female 交集處的資料格會顯示 Null。 同樣地，Abigail Clark 和 Male 交集處的資料格也會顯示 Null。 這些資料格不存在，也不包含值，但在查詢傳回的結果中會出現不存在的資料格。  
  
 當您使用 [Crossjoin (MDX)](../../../mdx/crossjoin-mdx.md) 函數傳回相同維度中多個屬性階層之成員的交叉乘積時，自動存在功能會將所傳回的 Tuple 限制於實際存在的 Tuple 集合，而不會傳回整個笛卡兒乘積。 例如，執行下列查詢，然後檢查執行的結果。  
  
```  
SELECT CROSSJOIN  
   (  
      {[Customer].[Country].[United States]},  
         [Customer].[State-Province].Members  
  ) ON 0   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
> [!NOTE]  
>  請注意，0 是用來指定資料行軸，為 axis(0) (即資料行軸) 的縮寫。  
  
 上述查詢只會針對查詢中每個屬性階層之同時存在的成員傳回資料格。 上述查詢也可以使用 [* (Crossjoin) (MDX)](../../../mdx/crossjoin-mdx-operator-reference.md) 函數中新的 * 變數，改寫如下。  
  
```  
SELECT   
   [Customer].[Country].[United States] *   
      [Customer].[State-Province].Members  
ON 0   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
 上述查詢也可以撰寫成下列方式：  
  
```  
SELECT [Customer].[State-Province].Members  
ON 0   
FROM [Adventure Works]  
WHERE (Measures.[Internet Sales Amount],  
   [Customer].[Country].[United States])  
```  
  
 所傳回的資料格值將會相同，不過結果集中的中繼資料將會不同。 例如，在上述查詢中，Country 階層已移至 slicer 座標軸 (在 WHERE 子句中)，因此不會明確出現在結果集中。  
  
 上述這三個查詢示範了 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中自動存在行為的作用。  
  
## <a name="user-defined-hierarchies-and-cube-space"></a>使用者自訂階層和 Cube 空間  
 在本主題的先前範例中，我們都是使用屬性階層來定義 Cube 空間中的位置。 然而，您也可以利用使用者自訂階層 (已經根據維度中的屬性階層加以定義)，定義 Cube 空間中的位置。 使用者自訂階層是由屬性階層組成的階層，設計目的為幫助使用者瀏覽 Cube 資料。  
  
 例如，上節中的 **CROSSJOIN** 查詢也可以撰寫如下：  
  
```  
SELECT CROSSJOIN  
   (  
      {[Customer].[Country].[United States]},  
         [Customer].[Customer Geography].[State-Province].Members  
   )   
ON 0   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
 在上述查詢中，Customer 維度內的 Customer Geography 使用者自訂階層是用來定義 Cube 空間中的位置 (先前是使用屬性階層加以定義)。 使用屬性階層或使用者自訂階層，都可以定義 Cube 空間中的相同位置。  
  
##  <a name="AttribRelationships"></a> 屬性關聯性和 Cube 空間  
 定義相關屬性之間的屬性關聯性後，不僅查詢效能會因著建立適當彙總而提高，與屬性階層成員同時出現的相關屬性階層成員也會因此受影響。 例如，當您定義的 Tuple 包含 City 屬性階層的成員，並且該 Tuple 沒有明確定義 Country 屬性階層成員，您可能預期預設的 Country 屬性階層成員將會是 Country 屬性階層的相關成員。 然而，只有在 City 屬性階層和 Country 屬性階層之間已定義屬性關聯性時，這個狀況才會屬實。  
  
 下列範例會傳回查詢中沒有明確包含之相關屬性階層的成員。  
  
```  
WITH MEMBER Measures.x AS   
   Customer.Country.CurrentMember.Name  
SELECT Measures.x ON 0,  
Customer.City.Members ON 1  
FROM [Adventure Works]  
```  
  
> [!NOTE]  
>  請注意，**WITH** 關鍵字是與 [CurrentMember (MDX)](../../../mdx/currentmember-mdx.md) 和 [Name (MDX)](../../../mdx/name-mdx.md) 函數搭配使用，可建立查詢中所使用的導出成員。 如需詳細資訊，請參閱[基本 MDX 查詢 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-the-basic-query.md)。  
  
 在上述查詢中，會傳回與 State 屬性階層之每個成員相關的 Country 屬性階層的成員名稱。 預期的 Country 成員會出現 (因為 City 和 Country 屬性之間已定義屬性關聯性)。 然而，如果相同維度中的多個屬性階層之間沒有定義屬性關聯性，則會傳回 (全部) 成員，如下列查詢所說明。  
  
```  
WITH MEMBER Measures.x AS   
   Customer.Education.Currentmember.Name  
SELECT Measures.x  ON 0,   
Customer.City.Members ON 1  
FROM [Adventure Works]  
```  
  
 在上述查詢中，會傳回 (全部) 成員 ("All Customers")，因為 Education 和 City 之間沒有關聯性。 因此，在包含 City 屬性階層但沒有明確提供 Education 成員的任何 Tuple 中，Education 屬性階層的 (全部) 成員將會是 Education 屬性階層的預設成員。  
  
## <a name="calculation-context"></a>計算內容  
  
## <a name="see-also"></a>另請參閱  
 [MDX 的關鍵概念 &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)   
 [Tuples](../../../analysis-services/multidimensional-models/mdx/tuples.md)   
 [自動存在](../../../analysis-services/multidimensional-models/mdx/autoexists.md)   
 [使用成員、Tuple 和集合 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md)   
 [視覺化總計和非視覺化總計](../../../analysis-services/multidimensional-models/mdx/visual-totals-and-non-visual-totals.md)   
 [MDX 語言參考 &#40;MDX&#41;](../../../mdx/mdx-language-reference-mdx.md)   
 [多維度運算式 &#40;MDX&#41 參考](../../../mdx/multidimensional-expressions-mdx-reference.md)  
  
  
