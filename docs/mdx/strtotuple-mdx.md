---
title: StrToTuple （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 232d1e94892165430867ec5217f8c87ccd625b48
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68036710"
---
# <a name="strtotuple-mdx"></a>StrToTuple (MDX)


  傳回由多維度運算式（MDX）格式化字串所指定的元組。  
  
## <a name="syntax"></a>語法  
  
```  
  
StrToTuple(Tuple_Specification [,CONSTRAINED] )   
```  
  
## <a name="arguments"></a>引數  
 *Tuple_Specification*  
 直接或間接指定 Tuple 的有效字串運算式。  
  
## <a name="remarks"></a>備註  
 **StrToTuple**函數會傳回指定的集合。 **StrToTuple**函數通常會搭配使用者自訂函數使用，將來自外部函數的元組規格傳回至 MDX 語句。  
  
-   使用 CONSTRAINED 旗標時，Tuple 規格必須包含限定或未限定成員名稱。 這個旗標用於降低遭到由指定字串發動資料隱碼攻擊的風險。 如果所提供的字串不能直接解析成限定或未限定成員名稱，會出現下列錯誤：「違反了 STRTOTUPLE 函數中 CONSTRAINED 旗標所加諸的限制。」  
  
-   沒有使用 CONSTRAINED 旗標時，指定的 Tuple 會解析成傳回 Tuple 的有效 MDX 運算式。  
  
## <a name="examples"></a>範例  
 下列範例會傳回 2004 日曆年度 Bayern 成員的 Reseller Sales Amount 量值。 所提供的 Tuple 規格包含有效 MDX Tuple 運算式。  
  
```  
SELECT StrToTuple ('([Geography].[State-Province].[Bayern],[Date].[Calendar Year].[CY 2004], [Measures].[Reseller Sales Amount])')  
ON 0  
FROM [Adventure Works]  
  
```  
  
 下列範例會傳回 2004 日曆年度 Bayern 成員的 Reseller Sales Amount 量值。 所提供的 Tuple 規格包含 CONSTRAINED 旗標所需的限定成員名稱。  
  
```  
SELECT StrToTuple ('([Geography].[State-Province].[Bayern],[Date].[Calendar Year].[CY 2004], [Measures].[Reseller Sales Amount])', CONSTRAINED)  
ON 0  
FROM [Adventure Works]  
  
```  
  
 下列範例會傳回 2004 日曆年度 Bayern 成員的 Reseller Sales Amount 量值。 所提供的 Tuple 規格包含有效 MDX Tuple 運算式。  
  
```  
SELECT StrToTuple ('([Geography].[State-Province].[Bayern],[Date].[Calendar Year].&[2003].NEXTMEMBER, [Measures].[Reseller Sales Amount])')  
ON 0  
FROM [Adventure Works]  
  
```  
  
 下列範例傳回因為 CONSTRAINED 旗標而發生的錯誤。 雖然所提供的 Tuple 規格包含有效 MDX Tuple 運算式，但 CONSTRAINED 旗標要求 Tuple 規格中包含限定或未限定成員名稱。  
  
```  
SELECT StrToTuple ('([Geography].[State-Province].[Bayern],[Date].[Calendar Year].&[2003].NEXTMEMBER, [Measures].[Reseller Sales Amount])', CONSTRAINED)  
ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
