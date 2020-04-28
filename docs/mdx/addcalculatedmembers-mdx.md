---
title: AddCalculatedMembers （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 982484b729b59a7106b6195e361110c1d4012653
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68017180"
---
# <a name="addcalculatedmembers-mdx"></a>AddCalculatedMembers (MDX)


  傳回藉由在指定集合中新增導出成員的方式所產生的集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
AddCalculatedMembers(Set_Expression)   
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 根據預設，MDX 會在解析集合函數時排除導出成員。 **AddCalculatedMembers**函數會檢查 Set_Expression 中指定的集合運算式 *，* 並包含屬於該集合運算式範圍內之成員的的匯出成員。  
  
> [!NOTE]  
>  此函數僅能搭配一維的集合運算式使用。  
  
## <a name="examples"></a>範例  
 以下範例示範此函數的用法。  
  
```  
-- This query returns the calculated members for the cube  
-- by retrieving all members, and then excluding non-calculated members.  
SELECT   
   AddCalculatedMembers(  
      {[Measures].Members}  
      )-[Measures].Members ON COLUMNS  
FROM [Adventure Works]   
```  
  
 除了 [**量值**] `Measures.[Unit Price]`維度中的所有匯出成員之外，下列範例也會從 [**艾德工作**] cube 傳回成員。  
  
```  
SELECT  
   AddCalculatedMembers({Measures.[Unit Price]}) ON COLUMNS  
FROM   
   [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
