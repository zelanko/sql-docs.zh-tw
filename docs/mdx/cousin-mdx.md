---
title: Cousin (MDX) |Microsoft 文件
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- COUSIN
dev_langs:
- kbMDX
helpviewer_keywords:
- Cousin function
ms.assetid: 9a416685-d35d-4d9c-a9f6-4574cbe59aea
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 30bfe88ded0c5723a673b4a99d89451339aadbd2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="cousin-mdx"></a>Cousin (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
 [MDX 函數參考 & #40;MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
