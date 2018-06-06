---
title: EXISTING 關鍵字 (MDX) |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 08cdfd62f25ec42195418938da37c502f221120d
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="mdx-query---existing-keyword"></a>MDX 查詢-EXISTING 關鍵字
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  強制在目前內容內評估指定的集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
Existing Set_Expression  
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression*  
 有效的多維度運算式 (MDX) 集合運算式。  
  
## <a name="remarks"></a>備註  
 根據預設，會在包含集合成員的 Cube 內容內評估集合。 但是 **Existing** 關鍵字會強制在目前的內容內評估指定的集合。  
  
## <a name="example"></a>範例  
 下列範例會根據使用 **Aggregate** 函數評估之使用者選取的 State-Province 成員值，傳回上一個時間週期銷售值衰退的轉售商計數。 但是 [Hierarchize &#40;MDX&#41;](../../../mdx/hierarchize-mdx.md) 和 [DrilldownLevel (MDX)](../../../mdx/drilldownlevel-mdx.md) 函數是用來傳回 Product 維度中產品類別目錄的衰退銷售值。 **Existing** 關鍵字會強制 **Filter** 函數中的集合在目前內容中評估，亦即針對 State-Province 屬性階層的 Washington 和 Oregon 成員。  
  
```  
WITH MEMBER Measures.[Declining Reseller Sales] AS  
   Count  
      (Filter  
         (Existing  
            (Reseller.Reseller.Reseller)  
         , [Measures].[Reseller Sales Amount] <   
            ([Measures].[Reseller Sales Amount]  
               ,[Date].Calendar.PrevMember  
            )  
        )  
      )  
MEMBER [Geography].[State-Province].x AS   
   Aggregate   
      ( {[Geography].[State-Province].&[WA]&[US]  
         , [Geography].[State-Province].&[OR]&[US] }   
      )  
SELECT NON EMPTY HIERARCHIZE   
      (AddCalculatedMembers   
         (   
            {DrillDownLevel  
               ({[Product].[All Products]}  
               )  
            }   
         )   
      ) DIMENSION PROPERTIES PARENT_UNIQUE_NAME ON COLUMNS   
FROM [Adventure Works]  
WHERE   
      ( [Geography].[State-Province].x  
        , [Date].[Calendar].[Calendar Quarter].&[2003]&[4]  
        ,[Measures].[Declining Reseller Sales]  
      )  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [計數 & #40;設定 & #41;& #40;MDX & #41;](../../../mdx/count-set-mdx.md)   
 [AddCalculatedMembers & #40;MDX & #41;](../../../mdx/addcalculatedmembers-mdx.md)   
 [彙總 & #40;MDX & #41;](../../../mdx/aggregate-mdx.md)   
 [篩選 & #40;MDX & #41;](../../../mdx/filter-mdx.md)   
 [屬性 & #40;MDX & #41;](../../../mdx/properties-mdx.md)   
 [DrilldownLevel & #40;MDX & #41;](../../../mdx/drilldownlevel-mdx.md)   
 [Hierarchize & #40;MDX & #41;](../../../mdx/hierarchize-mdx.md)   
 [MDX 函數參考 & #40;MDX & #41;](../../../mdx/mdx-function-reference-mdx.md)  
  
  
