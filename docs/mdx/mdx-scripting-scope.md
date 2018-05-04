---
title: SCOPE 陳述式 (MDX) |Microsoft 文件
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SCOPE
dev_langs:
- kbMDX
helpviewer_keywords:
- scope [MDX]
- SCOPE statement
ms.assetid: ceab459d-b601-4468-b3fc-4f5bb4a1805f
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 7cb864de089645a137676d7d8607e988e084939e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="mdx-scripting---scope"></a>MDX 指令碼-範圍
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
 SCOPE 陳述式會建立 subcube，不論公開 「 洞 」 **MDX 相容性**設定。 例如，陳述式 `Scope( Customer.State.members )` 可以包括不含州/省 (但已插入不可見的預留位置成員) 之國家 (地區) 中的州/省。  
  
 SCOPE 陳述式內建立的導出成員與命名集，不會受到 SCOPE 陳述式的影響。  
  
## <a name="example"></a>範例  
 下列範例中的，從 MDX 計算指令碼，在 Adventure Works 範例方案中，將目前的範圍為 2005年會計年度銷售量配額量值中的會計季度定義，然後將指定要使用目前的範圍中的資料格的值**ParallelPeriod**函式。 此範例接著會使用另一個 SCOPE 陳述式，範圍內修改，然後執行 另一個作業使用[This (MDX)](../mdx/this-mdx.md)函式。  
  
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
 [MDX 指令碼陳述式 & #40;MDX & #41;](../mdx/mdx-scripting-statements-mdx.md)  
  
  
