---
title: StrToMember (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0c5878a553895dccc3350ddbae9397d5a48c6349
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52531210"
---
# <a name="strtomember-mdx"></a>StrToMember (MDX)


  傳回多維度運算式 (MDX） 格式化的字串所指定的成員。  
  
## <a name="syntax"></a>語法  
  
```  
  
StrToMember(Member_Name [,CONSTRAINED] )   
```  
  
## <a name="arguments"></a>引數  
 *Member_Name*  
 直接或間接指定成員的有效字串運算式。  
  
## <a name="remarks"></a>備註  
 **StrToMember**函式會傳回字串運算式中指定的成員。 **StrToMember**函式通常搭配使用者自訂函數用來從外部函式中的成員規格傳回至 MDX 陳述式或 MDX 查詢參數化。  
  
-   使用 CONSTRAINED 旗標時，成員名稱必須可直接解析成合格的或不合格的成員名稱。 這個旗標用於降低遭到由指定字串發動資料隱碼攻擊的風險。 如果所提供，不能直接解析成限定或未限定成員名稱的字串，則會出現下列錯誤：「 CONSTRAINED 所加諸的限制違反了 STRTOMEMBER 函數中的旗標。 」  
  
-   沒有使用 CONSTRAINED 旗標時，指定的成員可以直接解析為成員名稱，或解析成會解析成名稱的 MDX 運算式。  
  
-   若要進一步了解集合和成員之間的差異，請參閱＜使用集合運算式＞和＜使用成員運算式＞。  
  
## <a name="examples"></a>範例  
 下列範例會傳回使用 State-province 屬性階層中 Bayern 成員的 Reseller Sales Amount 量值**StrToMember**函式。 指定的字串提供了限定成員名稱。  
  
```  
SELECT {StrToMember ('[Geography].[State-Province].[Bayern]')}  
ON 0,  
{[Measures].[Reseller Sales Amount]} ON 1  
FROM [Adventure Works]  
  
```  
  
 下列範例會傳回使用 Bayern 成員的 Reseller Sales Amount 量值**StrToMember**函式。 因為成員名稱字串只提供不合格的成員名稱，所以查詢會傳回指定成員的第一個執行個體，這正好是在 Customer 維度的 Customer Geography 階層中，與 Reseller Sales 沒有交集。 最佳做法應規定指定合格的名稱，以確保預期的結果。  
  
```  
SELECT {StrToMember ('[Bayern]').Parent}  
ON 0,  
{[Measures].[Reseller Sales Amount]} ON 1  
FROM [Adventure Works]  
  
```  
  
 下列範例會傳回使用 State-province 屬性階層中 Bayern 成員的 Reseller Sales Amount 量值**StrToMember**函式。 所提供的成員名稱字串會解析成合格的成員名稱。  
  
```  
SELECT {StrToMember('[Geography].[Geography].[Country].[Germany].FirstChild', CONSTRAINED)}  
ON 0,  
{[Measures].[Reseller Sales Amount]} ON 1  
FROM [Adventure Works]  
  
```  
  
 下列範例傳回因為 CONSTRAINED 旗標而發生的錯誤。 雖然所提供的成員名稱字串包含會解析成限定成員名稱的有效 MDX 成員運算式，但 CONSTRAINED 旗標要求成員名稱字串中包含限定或未限定成員名稱。  
  
```  
SELECT StrToMember ('[Geography].[Geography].[Country].[Germany].FirstChild', CONSTRAINED)  
ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
