---
title: 產生（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c7a6008129d6b0a4c59412428c31f6e5de625f1f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68005901"
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
 如果指定第二個集合，則**產生**函數會傳回一個集合，其方式是將第二個集合中的元組套用至第一個集合中的每個元組，然後依 union 聯結產生的集合。 如果指定**ALL** ，則函式會在結果集中保留重複的專案。  
  
 如果指定字串運算式，則**產生**函數會傳回一個字串，方法是針對第一個集合中的每個元組評估指定的字串運算式，然後串連結果。 另外，也可以選擇字串分隔符號，在產生的串連字串中分隔每個結果。  
  
## <a name="examples"></a>範例  
  
### <a name="set"></a>設定  
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
  
 「**產生**」最常見的實際用法是針對一組成員評估複雜的集合運算式，例如 TopCount。 下列範例查詢會針對資料列上的每一個 Calendar Year 顯示前 10 大產品：  
  
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
  
 請注意，每年會顯示不同的前10個，而且使用 [**產生**] 是取得此結果的唯一方式。 只是交叉聯結 Calendar Years 以及前 10 大產品集合將會顯示所有年度的前 10 大產品，每一年都會重複，如以下範例所示：  
  
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
 下列範例示範如何使用「**產生**」來傳回字串：  
  
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
>  這種形式的**產生**函數在偵測計算時很有用，因為它可讓您傳回字串，以顯示集合中所有成員的名稱。 這可能比[SetToStr &#40;MDX&#41;](../mdx/settostr-mdx.md)函式所傳回之集合的嚴格 MDX 表示方式更容易閱讀。  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
