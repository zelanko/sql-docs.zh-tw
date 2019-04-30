---
title: DataMember (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 98b10c951043416280c05fd6a0e5eeb5df92c104
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63248136"
---
# <a name="datamember-mdx"></a>DataMember (MDX)


  傳回由系統所產生，與維度某個非分葉成員相關的資料成員。  
  
## <a name="syntax"></a>語法  
  
```  
  
Member_Expression.DataMember  
```  
  
## <a name="arguments"></a>引數  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 此函式會在所有階層架構中的非分葉成員上運作，並可供[UPDATE CUBE 陳述式 (MDX)](../mdx/mdx-data-manipulation-update-cube.md)命令給非分葉成員直接，而不是分葉成員的下階的回寫資料。  
  
> [!NOTE]  
>  如果指定的成員是分葉成員，或如果非分葉成員沒有相關聯的資料成員，就會傳回指定的成員。  
  
## <a name="example"></a>範例  
 下列範例會使用**DataMember**中顯示的銷售配額每個員工的導出量值函式：  
  
```  
WITH MEMBER measures.InvidualQuota AS   
([Employee].[Employees].currentmember.datamember, [Measures].[Sales Amount Quota])  
,FORMAT_STRING='Currency'  
SELECT {[Measures].[Sales Amount Quota],[Measures].InvidualQuota} ON COLUMNS,  
[Employee].[Employees].MEMBERS ON ROWS  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [MDX 的關鍵概念 &#40;Analysis Services&#41;](../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)  
  
  
