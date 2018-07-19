---
title: StrToValue (MDX) |Microsoft 文件
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5a46b68ac8e93a00c7730b32593331a28655c1c5
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2018
ms.locfileid: "34743067"
---
# <a name="strtovalue-mdx"></a>StrToValue (MDX)


  傳回由多維度運算式 (MDX) 格式化字串指定的數值。  
  
## <a name="syntax"></a>語法  
  
```  
  
StrToValue(MDX_Expression [,CONSTRAINED] )   
```  
  
## <a name="arguments"></a>引數  
 *MDX_Expression*  
 直接或間接解析成單一資料格的有效字串運算式。  
  
## <a name="remarks"></a>備註  
 **StrToValue**函式會傳回數值 MDX 運算式所指定。 **StrToValue**函式通常用於搭配使用者自訂函數來自外部函數的 MDX 運算式傳回至 MDX 陳述式，是可解析成單一資料格。  
  
-   使用 CONSTRAINED 旗標時，MDX 運算式只能包含純量值。 CONSTRAINED 旗標是用來降低由指定字串發動資料隱碼攻擊的風險。 如果所提供的 MDX 運算式不能直接解析成純量值，會出現下列錯誤：「違反了 STRTOVALUE 函數中 CONSTRAINED 旗標所加諸的限制。」  
  
-   沒有使用 CONSTRAINED 旗標時，指定的 MDX 運算式可依需要盡可能複雜，只要它能解析成傳回單一資料格的有效多維度運算式 (MDX) 運算式。  
  
> [!NOTE]  
>  如果值是儲存成文字，並且您要在傳回值上執行算術運算時，傳回 MDX 運算式的結果做為數值會很有用。  
  
## <a name="example"></a>範例  
 下列範例會使用**StrToValue**函數來傳回每輛腳踏車做為值的加權。  
  
```  
WITH MEMBER Measures.x AS   
StrToValue   
   ([Product].[Product].CurrentMember.Properties ('Weight')  
   ,CONSTRAINED  
   )  
SELECT Measures.x ON 0  
,[Product].[Product].[Product].Members ON 1  
FROM [Adventure Works]  
WHERE [Product].[Product Categories].[Bikes]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
