---
title: 產生 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 222479dd03263f61a603e30202f2abf54307b0bc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63224886"
---
# <a name="generate-mdx"></a>Generate (MDX)


  套用一個集合到另一個集合的每個成員，然後以聯集的方式將結果集聯結。 或者，針對集合進行字串運算式評估之後，傳回所產生的串連字串。  
  
## <a name="syntax"></a>語法  
  
```  
  
Set expression syntax  
Generate( Set_Expression1 ,  Set_Expression2 [ , ALL ]  )  
  
String expression syntax  
Generate( Set_Expression1 ,  String_Expression [ ,Delimiter ]  )  
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression1*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *Set_Expression2*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *String_Expression*  
 有效的字串運算式，這通常是指定集合中每個 Tuple 的目前成員名稱 (CurrentMember.Name)。  
  
 *分隔符號*  
 以字串運算式表示的有效分隔符號。  
  
## <a name="remarks"></a>備註  
 如果未指定第二個集合，則**Generate**函式會傳回所將套用至第一個集合中的每個 tuple 的第二個集合中的 tuple 產生一組 *，* 和聯集，然後將聯結所產生的設定。 如果**所有**指定，則此函式會保留在結果集中的重複項。  
  
 如果指定的字串運算式，則**Generate**函式會傳回所指定的字串運算式，對第一個集合中的每個 tuple 評估產生的字串 *，* 然後串連結果。 另外，也可以選擇字串分隔符號，在產生的串連字串中分隔每個結果。  
  
## <a name="examples"></a>範例  
  
### <a name="set"></a>將  
 在以下範例中，查詢會傳回包含 Measure Internet Sales 數量四次的集合，因為 [Date].[Calendar Year].[Calendar Year].MEMBERS 集合中有四個成員：  
  
```  
SELECT   
GENERATE( [Date].[Calendar Year].[Calendar Year].MEMBERS  
, {[Measures].[Internet Sales Amount]}, ALL)  
ON 0  
FROM [Adventure Works]  
```  
  
 移除 ALL 會變更此查詢，好讓 Internet Sales Amount 只傳回一次：  
  
```  
SELECT   
GENERATE( [Date].[Calendar Year].[Calendar Year].MEMBERS  
, {[Measures].[Internet Sales Amount]})  
ON 0  
FROM [Adventure Works]  
```  
  
 最常見的實際用法**產生**評估複雜設定成員的集合運算式，例如 TopCount。 下列範例查詢會針對資料列上的每一個 Calendar Year 顯示前 10 大產品：  
  
```  
SELECT   
{[Measures].[Internet Sales Amount]}  
ON 0,  
GENERATE(   
[Date].[Calendar Year].[Calendar Year].MEMBERS  
, TOPCOUNT(  
[Date].[Calendar Year].CURRENTMEMBER  
*  
[Product].[Product].[Product].MEMBERS  
,10, [Measures].[Internet Sales Amount]))  
ON 1  
FROM [Adventure Works]  
```  
  
 請注意，不同的前 10 個會顯示每年，而且使用**產生**是唯一的方法來取得這個結果。 只是交叉聯結 Calendar Years 以及前 10 大產品集合將會顯示所有年度的前 10 大產品，每一年都會重複，如以下範例所示：  
  
```  
SELECT   
{[Measures].[Internet Sales Amount]}  
ON 0,  
[Date].[Calendar Year].[Calendar Year].MEMBERS  
*   
TOPCOUNT(  
[Product].[Product].[Product].MEMBERS  
,10, [Measures].[Internet Sales Amount])  
ON 1  
FROM [Adventure Works]  
```  
  
### <a name="string"></a>String  
 下列範例示範使用**產生**傳回的字串：  
  
```  
WITH   
MEMBER MEASURES.GENERATESTRINGDEMO AS  
GENERATE(   
[Date].[Calendar Year].[Calendar Year].MEMBERS,  
[Date].[Calendar Year].CURRENTMEMBER.NAME)  
MEMBER MEASURES.GENERATEDELIMITEDSTRINGDEMO AS  
GENERATE(   
[Date].[Calendar Year].[Calendar Year].MEMBERS,  
[Date].[Calendar Year].CURRENTMEMBER.NAME, " AND ")  
SELECT   
{MEASURES.GENERATESTRINGDEMO, MEASURES.GENERATEDELIMITEDSTRINGDEMO}  
ON 0  
FROM [Adventure Works]  
```  
  
> [!NOTE]  
>  這種**產生**函式有助於進行偵錯計算，因為它可讓您傳回集合中顯示的所有成員名稱的字串。 這可能是更方便閱讀比一組嚴格 MDX 表示法， [SetToStr &#40;MDX&#41; ](../mdx/settostr-mdx.md)函式會傳回。  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
