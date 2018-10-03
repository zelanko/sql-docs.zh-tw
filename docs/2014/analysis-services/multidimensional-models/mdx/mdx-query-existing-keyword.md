---
title: EXISTING 關鍵字 (MDX) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- EXISTING
helpviewer_keywords:
- Existing keyword
ms.assetid: 651ee9ac-04ef-4316-87c9-a3df5ac27d22
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8431c4b29f20b3c87e3b944736612d009426900a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48106548"
---
# <a name="existing-keyword-mdx"></a>EXISTING 關鍵字 (MDX)
  強制在目前內容內評估指定的集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
Existing Set_Expression  
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression*  
 有效的多維度運算式 (MDX) 集合運算式。  
  
## <a name="remarks"></a>備註  
 根據預設，會在包含集合成員的 Cube 內容內評估集合。 `Existing`關鍵字會強制改為評估目前內容中指定的集合。  
  
## <a name="example"></a>範例  
 下列範例會根據使用 `Aggregate` 函數評估之使用者選取的 State-Province 成員值，傳回上一個時間週期銷售值衰退的轉售商計數。 但是 [Hierarchize &#40;MDX&#41;](/sql/mdx/hierarchize-mdx) 和 [DrilldownLevel (MDX)](/sql/mdx/drilldownlevel-mdx) 函數是用來傳回 Product 維度中產品類別目錄的衰退銷售值。 `Existing`關鍵字會強制中設定的`Filter`State-province 屬性階層的 Washington 和 Oregon 成員目前內容中-也就是要評估的函式。  
  
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
 [計數&#40;設定&#41; &#40;MDX&#41;](/sql/mdx/count-set-mdx)   
 [AddCalculatedMembers &#40;MDX&#41;](/sql/mdx/addcalculatedmembers-mdx)   
 [彙總&#40;MDX&#41;](/sql/mdx/aggregate-mdx)   
 [篩選&#40;MDX&#41;](/sql/mdx/filter-mdx)   
 [屬性&#40;MDX&#41;](/sql/mdx/properties-mdx)   
 [DrilldownLevel &#40;MDX&#41;](/sql/mdx/drilldownlevel-mdx)   
 [Hierarchize &#40;MDX&#41;](/sql/mdx/hierarchize-mdx)   
 [MDX 函數參考&#40;MDX&#41;](/sql/mdx/mdx-function-reference-mdx)  
  
  
