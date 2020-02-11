---
title: UnknownMember （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: a0332b200a74044dcd4e7d8d308923cc4b759738
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68097277"
---
# <a name="unknownmember-mdx"></a>UnknownMember (MDX)


  傳回與層級或成員相關的未知的成員。  
  
## <a name="syntax"></a>語法  
  
```  
  
Member expression syntax  
Member_Expression.UnknownMember  
  
Hierarchy_expression syntax  
Hierarchy_Expression.UnknownMember  
```  
  
## <a name="arguments"></a>引數  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
 *Hierarchy_Expression*  
 傳回階層的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 Analysis Services 建立未知的成員，以便在不知道階層時，將事實資料表資料與階層產生關聯。 未知的成員可位於以下其中一個層級：  
  
-   無法彙總之屬性階層的最上層。  
  
-   在自然階層的 [**全部**] 層級底下的第一個層級。  
  
-   非自然階層的任何層級。  
  
 如果已指定成員運算式， **UnknownMember**函數會傳回指定成員的未知成員子系。 如果指定的成員不存在，此函數會傳回 Null。  
  
 如果指定了階層運算式， **UnknownMember**函數會在最上層傳回未知的成員（如果有的話）。  
  
 如果層級或成員上沒有未知的成員存在， **UnknownMember**函數會建立 null 成員。  
  
> [!NOTE]  
>  如果階層或成員上沒有未知的成員存在，就會產生一個錯誤。  
  
## <a name="examples"></a>範例  
 下列範例會為 Measures 維度的所有成員傳回 Product 屬性階層中 All Products 成員的未知成員。  
  
```  
SELECT [Product].[Product].[All Products].UnknownMember  
    ON Columns,  
[Measures].Members  
    ON Rows  
FROM [Adventure Works]  
  
```  
  
 下列範例會為 Measures 維度的所有成員傳回 Product Categories 階層的未知成員。  
  
```  
SELECT [Product].[Product Categories].UnknownMember  
    ON Columns,  
[Measures].Members  
    ON Rows  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [Mdx 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
