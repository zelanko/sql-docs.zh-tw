---
description: DataMember (MDX)
title: DataMember (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ea373dc4ffe7eb01b19969288afce45489ab4e8c
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196032"
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
 此函式會在任何階層中的非分葉成員上運作，而且可供 [UPDATE CUBE 語句 (MDX) ](../mdx/mdx-data-manipulation-update-cube.md) 命令，直接將資料回寫至非分葉成員，而不是分葉成員的子系。  
  
> [!NOTE]  
>  如果指定的成員是分葉成員，或如果非分葉成員沒有相關聯的資料成員，就會傳回指定的成員。  
  
## <a name="example"></a>範例  
 下列範例會在匯出量值中使用 **DataMember** 函數，以顯示每個個別員工的銷售配額：  
  
```  
WITH MEMBER measures.InvidualQuota AS   
([Employee].[Employees].currentmember.datamember, [Measures].[Sales Amount Quota])  
,FORMAT_STRING='Currency'  
SELECT {[Measures].[Sales Amount Quota],[Measures].InvidualQuota} ON COLUMNS,  
[Employee].[Employees].MEMBERS ON ROWS  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [Mdx 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [MDX 的關鍵概念 &#40;Analysis Services&#41;](/analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services)  
  
