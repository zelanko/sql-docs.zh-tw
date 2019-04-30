---
title: LookupCube (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8f8338a542bf9e15816205930704c45a536a5629
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63208511"
---
# <a name="lookupcube-mdx"></a>LookupCube (MDX)


  在評估過相同資料庫中其他指定的 Cube 之後，傳回多維度運算式 (MDX) 運算式的值。  
  
## <a name="syntax"></a>語法  
  
```  
  
Numeric expression syntax  
LookupCube(Cube_Name, Numeric_Expression )  
  
String expression syntax  
LookupCube(Cube_Name, String_Expression )  
```  
  
## <a name="arguments"></a>引數  
 *Cube_Name*  
 指定 Cube 名稱的有效字串運算式。  
  
 *Numeric_Expression*  
 有效的數值運算式，這通常是傳回數字之資料格座標的多維度運算式 (MDX) 運算式。  
  
 *String_Expression*  
 有效的字串運算式，這通常是傳回字串之資料格座標的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 如果指定數值運算式，則**LookupCube**函式會評估指定的 cube 中指定之數值運算式，並傳回產生的數字值。  
  
 如果指定的字串運算式，則**LookupCube**函式會評估指定的 cube 中的指定的字串運算式，並傳回結果的字串值。  
  
 **LookupCube**函式的運作方式相同資料庫內的 cube 所在之 MDX 查詢的來源 cube 包含**LookupCube**函式執行。  
  
> [!IMPORTANT]  
>  您必須在數值或字串運算式中提供任何必要的目前成員，因為目前查詢的內容不會延續至所查詢的 Cube。  
  
 使用任何計算**LookupCube**函式都可能會發生效能不彰。 請考慮重新設計方案，讓所有必要資料出現在一個 Cube 中，而不要使用這個函數。  
  
## <a name="examples"></a>範例  
 下列查詢會示範 LookupCube 的使用：  
  
 `WITH MEMBER MEASURES.LOOKUPCUBEDEMO AS`  
  
 `LOOKUPCUBE("Adventure Works", "[Measures].[In" + "ternet Sales Amount]")`  
  
 `SELECT MEASURES.LOOKUPCUBEDEMO  ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
