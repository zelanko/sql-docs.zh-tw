---
title: StrToSet (MDX) |Microsoft 文件
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7184dc872624f6589ec6e93911b39c9f8b4e4aa3
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2018
ms.locfileid: "34742977"
---
# <a name="strtoset-mdx"></a>StrToSet (MDX)


  傳回由多維度運算式 (MDX) 指定的集合 –格式化字串。  
  
## <a name="syntax"></a>語法  
  
```  
  
StrToSet(Set_Specification [,CONSTRAINED] )   
```  
  
## <a name="arguments"></a>引數  
 *Set_Specification*  
 直接或間接指定集合的有效字串運算式。  
  
## <a name="remarks"></a>備註  
 **StrToSet**函式會傳回字串運算式中指定的集合。 **StrToSet**函式通常會搭配使用者自訂函數用來從外部函式中的集合規格傳回至 MDX 陳述式或 MDX 查詢參數化。  
  
-   使用 CONSTRAINED 旗標時，集合規格必須包含限定或未限定成員名稱或一組包含大括弧括住的限定或未限定成員名稱的 tuple {}。 這個旗標用於降低遭到由指定字串發動資料隱碼攻擊的風險。 如果所提供的字串不能直接解析成限定或未限定成員名稱，會出現下列錯誤：「違反了 STRTOSET 函數中 CONSTRAINED 旗標所加諸的限制。」  
  
-   沒有使用 CONSTRAINED 旗標時，指定的集合規格會解析成傳回集合的有效多維度運算式 (MDX) 運算式。  
  
-   若要進一步了解集合和成員之間的差異，請參閱＜使用集合運算式＞和＜使用成員運算式＞。  
  
## <a name="examples"></a>範例  
 下列範例會傳回 State-province 屬性階層使用的成員集合**StrToSet**函式。 集合規格提供有效 MDX 集合運算式。  
  
```  
SELECT StrToSet ('[Geography].[State-Province].Members')  
ON 0  
FROM [Adventure Works]  
  
```  
  
 下列範例傳回因為 CONSTRAINED 旗標而發生的錯誤。 雖然集合規格提供有效 MDX 集合運算式，但 CONSTRAINED 旗標需要集合規格中的限定或未限定成員名稱。  
  
```  
SELECT StrToSet ('[Geography].[State-Province].Members', CONSTRAINED)  
ON 0  
FROM [Adventure Works]  
  
```  
  
 下列範例會傳回德國和加拿大兩個國家 (地區) 的 Reseller Sales Amount 量值。 指定之字串中所提供的集合規格包含 CONSTRAINED 旗標所需的限定成員名稱。  
  
```  
SELECT StrToSet ('{[Geography].[Geography].[Country].[Germany],[Geography].[Geography].[Country].[Canada]}', CONSTRAINED)  
ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
