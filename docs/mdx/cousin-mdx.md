---
title: Cousin （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8a98d496467e2fd75924b0067257f192c79cdf6e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68047255"
---
# <a name="cousin-mdx"></a>Cousin (MDX)


  傳回在某父成員之下，與指定的子成員具有相同關係位置的子成員。  
  
## <a name="syntax"></a>語法  
  
```  
  
Cousin( Member_Expression , Ancestor_Member_Expression )  
```  
  
## <a name="arguments"></a>引數  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
 *Ancestor_Member_Expression*  
 傳回上階成員的有效多維度運算式 (MDX) 成員運算式。  
  
## <a name="remarks"></a>備註  
 這個函數會作用在層級內成員的順序與位置上。 若有兩個階層存在，第一個階層有 4 個層級，第二個階層有 5 個層級，則第一個階層第三個層級的 Cousin 就是第二個階層的第三個層級。  
  
## <a name="examples"></a>範例  
 下列範例會根據 2003 會計年度年層級的上階，擷取 2002 會計年度第四季的 Cousin。 所擷取的 Cousin 是 2003 會計年度第四季。  
  
```  
SELECT Cousin   
   ( [Date].[Fiscal].[Fiscal Quarter].[Q4 FY 2002],  
     [Date].[Fiscal].[FY 2003]  
   ) ON 0  
FROM [Adventure Works]  
```  
  
 下列範例會根據 2004 會計年度第二季季層級的上階，擷取 2002 會計年度 7 月份的 Cousin。 所擷取的 Cousin 是 2003 年 10 月。  
  
```  
SELECT Cousin   
   ([Date].[Fiscal].[Month].[July 2002] ,  
    [Date].[Fiscal].[Fiscal Quarter].[Q2 FY 2004]  
   ) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [Mdx 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
