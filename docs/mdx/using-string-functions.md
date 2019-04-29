---
title: 使用字串函數 |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6e151d06d086569b16fcdf1dc3570f9b220dfcd6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62928151"
---
# <a name="using-string-functions"></a>使用字串函數


  多維度運算式 (MDX) 中每個物件幾乎都可以使用字串函數。 在預存程序中，字串函數主要用來將物件轉換為字串表示法。 您也可以使用字串函數在物件上評估字串運算式，以傳回一個值。  
  
 最常用的字串函式**名稱**並**Uniquename**。 這些函數會分別傳回某個物件的名稱和唯一名稱。 它們大多用於偵錯計算來找出函數所傳回的成員。  
  
## <a name="examples"></a>範例  
 下列範例查詢會示範如何使用這些函數：  
  
 `WITH`  
  
 `//Returns the name of the current Product on rows`  
  
 `MEMBER [Measures].[ProductName] AS [Product].[Product].CurrentMember.Name`  
  
 `//Returns the uniquename of the current Product on rows`  
  
 `MEMBER [Measures].[ProductUniqueName] AS [Product].[Product].CurrentMember.Uniquename`  
  
 `//Returns the name of the Product dimension`  
  
 `MEMBER [Measures].[ProductDimensionName] AS [Product].Name`  
  
 `SELECT  {[Measures].[ProductName],[Measures].[ProductUniqueName],[Measures].[ProductDimensionName]}`  
  
 `ON COLUMNS,`  
  
 `[Product].[Product].MEMBERS  ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 **產生**函式可用來執行的一組每個成員的字串函數及串連結果。 這對於偵錯計算也很實用，因為它可讓您將集合的內容視覺化。 下列範例示範這種方式的作法：  
  
 `WITH`  
  
 `//Returns the names of the current Product and its ancestors up to the All Member`  
  
 `MEMBER [Measures].[AncestorNames] AS`  
  
 `GENERATE(`  
  
 `ASCENDANTS([Product].[Product Categories].CurrentMember)`  
  
 `, [Product].[Product Categories].CurrentMember.Name, ", ")`  
  
 `SELECT`  
  
 `{[Measures].[AncestorNames]}`  
  
 `ON COLUMNS,`  
  
 `[Product].[Product Categories].MEMBERS  ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 另一組常用的字串函數就是那些可讓您將包含物件或運算式 (可解析成物件) 之唯一名稱的字串轉換成物件本身的函數。 下列範例查詢示範如何**StrToMember**並**StrToSet**函式執行這項操作：  
  
 `SELECT`  
  
 `{StrToMember("[Measures].[Inter" + "net Sales Amount]")}`  
  
 `ON COLUMNS,`  
  
 `StrToSet("{`  
  
 `[Product].[Product Categories].[Category].&[3],`  
  
 `[Product].[Product Categories].[Product].&[477],`  
  
 `[Product].[Product Categories].[Product].&[788],`  
  
 `[Product].[Product Categories].[Product].&[708],`  
  
 `[Product].[Product Categories].[Product].&[711]`  
  
 `}")`  
  
 `ON ROWS`  
  
 `FROM [Adventure Works]`  
  
> [!NOTE]  
>  **StrToMember**並**StrToSet**函式應該謹慎使用。 因為如果在計算定義內使用它們，可能會產生極差的查詢效能。  
  
## <a name="see-also"></a>另請參閱  
 [產生&#40;MDX&#41;](../mdx/generate-mdx.md)   
 [Name &#40;MDX&#41;](../mdx/name-mdx.md)   
 [UniqueName &#40;MDX&#41;](../mdx/uniquename-mdx.md)   
 [函式&#40;MDX 語法&#41;](../mdx/functions-mdx-syntax.md)   
 [使用預存程序&#40;MDX&#41;](../mdx/using-stored-procedures-mdx.md)   
 [StrToMember &#40;MDX&#41;](../mdx/strtomember-mdx.md)   
 [StrToSet &#40;MDX&#41;](../mdx/strtoset-mdx.md)  
  
  
