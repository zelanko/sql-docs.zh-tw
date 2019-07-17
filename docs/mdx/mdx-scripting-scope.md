---
title: SCOPE 陳述式 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2f355842999b505a97c3387ab9e51d3b651c3b7c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138275"
---
# <a name="mdx-scripting---scope"></a>MDX 指令碼 - SCOPE


  將指定的多維度運算式 (MDX) 陳述式的範圍限制為指定的 Subcube。  
  
## <a name="syntax"></a>語法  
  
```  
  
SCOPE(Subcube_Expression)   
   [ MDX_Statement ]  
END SCOPE  
  
Subcube_Expression ::=(Auxiliary_Subcube [, Auxiliary_Subcube,...n])  
  
Auxiliary_Subcube ::=   
        Limited_Set   
    | Root([dimension_name])   
    | Leaves([dimension_name])  
  
Limited_Set ::=   
        single_tuple   
    | member   
    | Common_Grain_Members   
    | hierarchy.members   
    | level.members   
    | {}   
    | Descendants  
            (  
                  Member  
         , [level  
         [  
            , SELF   
             | AFTER   
                          | BEFORE   
                          | SELF_AND_AFTER   
                          | SELF_AND_BEFORE   
                          | SELF_BEFORE_AFTER   
                          | LEAVES  
                  ]  
            )   
[* <limited set>]  
```  
  
## <a name="arguments"></a>引數  
 *Subcube_Expression*  
 有效的 MDX Subcube 運算式。  
  
 *MDX_Statement*  
 有效的 MDX 陳述式。  
  
 *Common_Grain_Members*  
 一個有效 MDX 陳述式，將成員評估為擁有相同資料粒度。  
  
 *single_tuple*  
 單一 Tuple。  
  
## <a name="remarks"></a>備註  
 SCOPE 陳述式決定會受到執行一個或多個 MDX 陳述式影響的 Subcube。 除非 SCOPE 陳述式中嵌有 MDX 陳述式，否則 MDX 陳述式的隱含範圍是整個 Cube。  
  
> [!NOTE]  
>  隱藏 SCOPE 陳述式中公開的成員。  
  
 SCOPE 陳述式會建立 subcube，不論公開 「 洞孔 」 裡**MDX Compatibility**設定。 例如，陳述式 `Scope( Customer.State.members )` 可以包括不含州/省 (但已插入不可見的預留位置成員) 之國家 (地區) 中的州/省。  
  
 SCOPE 陳述式內建立的導出成員與命名集，不會受到 SCOPE 陳述式的影響。  
  
## <a name="example"></a>範例  
 下列範例中的，從 MDX 計算指令碼，在 Adventure Works 範例方案為 2005年會計年度和 [銷售量配額] 量中的會計季度定義目前的範圍，然後將值指派給目前的範圍中的資料格所使用的**ParallelPeriod**函式。 此範例接著會使用另一個 SCOPE 陳述式，範圍內修改，然後執行 另一個指派使用[This (MDX)](../mdx/this-mdx.md)函式。  
  
```  
Scope   
 (   
    [Date].[Fiscal Year].&[2005],  
    [Date].[Fiscal].[Fiscal Quarter].Members,  
    [Measures].[Sales Amount Quota]  
 ) ;     
  
   This = ParallelPeriod                               
          (   
             [Date].[Fiscal].[Fiscal Year], 1,  
             [Date].[Fiscal].CurrentMember   
          ) * 1.35 ;  
  
/*-- Allocate equally to months in FY 2002 -----------------------------*/  
  
  Scope   
  (   
     [Date].[Fiscal Year].&[2002],  
     [Date].[Fiscal].[Month].Members   
  ) ;     
  
    This = [Date].[Fiscal].CurrentMember.Parent / 3 ;     
  
  End Scope ;     
End Scope ;     
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 指令碼陳述式 &#40;MDX&#41;](../mdx/mdx-scripting-statements-mdx.md)  
  
  
