---
title: IsSibling (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d86c96686357533aa1217571f3c199ec8ddff508
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63125504"
---
# <a name="issibling-mdx"></a>IsSibling (MDX)


  傳回指定的成員是不是與另一個指定成員同層級。  
  
## <a name="syntax"></a>語法  
  
```  
  
IsSibling(Member_Expression1, Member_Expression2)   
```  
  
## <a name="arguments"></a>引數  
 *Member_Expression1*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
 *Member_Expression2*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 **IsSibling**函式會傳回 **，則為 true**如果第一個指定成員是第二個指定成員的同層級。 否則，函數會傳回**false**。  
  
## <a name="example"></a>範例  
 如果 Date 維度 Fiscal 階層上的目前成員是 2002 年 7 月的同層級，下列範例會傳回 TRUE：  
  
 `WITH MEMBER MEASURES.ISSIBLINGDEMO AS`  
  
 `IsSibling([Date].[Fiscal].CURRENTMEMBER, [Date].[Fiscal].[Month].&[2002]&[7])`  
  
 `SELECT {MEASURES.ISSIBLINGDEMO} ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
