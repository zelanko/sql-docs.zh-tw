---
description: LookupCube (MDX)
title: LookupCube (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d00f7cf0d657d2424b461ad95bc7f534cd2c33e8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88341472"
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
 如果指定了數值運算式， **LookupCube** 函數會在指定的 cube 中評估指定的數值運算式，並傳回產生的數值。  
  
 如果指定了字串運算式， **LookupCube** 函數會在指定的 cube 中評估指定的字串運算式，並傳回產生的字串值。  
  
 **LookupCube**函式適用于與來源 cube 相同資料庫內的 cube，其中包含**LOOKUPCUBE**函數的 MDX 查詢正在執行。  
  
> [!IMPORTANT]  
>  您必須在數值或字串運算式中提供任何必要的目前成員，因為目前查詢的內容不會延續至所查詢的 Cube。  
  
 使用 **LookupCube** 函數的任何計算都可能會受到效能不佳的影響。 請考慮重新設計方案，讓所有必要資料出現在一個 Cube 中，而不要使用這個函數。  
  
## <a name="examples"></a>範例  
 下列查詢會示範 LookupCube 的使用：  
  
 `WITH MEMBER MEASURES.LOOKUPCUBEDEMO AS`  
  
 `LOOKUPCUBE("Adventure Works", "[Measures].[In" + "ternet Sales Amount]")`  
  
 `SELECT MEASURES.LOOKUPCUBEDEMO  ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
