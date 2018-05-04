---
title: StrToMember (MDX) |Microsoft 文件
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
- STRTOMEMBER
dev_langs:
- kbMDX
helpviewer_keywords:
- StrToMember function
ms.assetid: eb8a3dc0-5ae4-434e-b321-680a81a59e67
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 32cd3674777bf309a9c23f9021208749c15d489f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="strtomember-mdx"></a>StrToMember (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  傳回由多維度運算式 (MDX) 指定的成員 –格式化字串。  
  
## <a name="syntax"></a>語法  
  
```  
  
StrToMember(Member_Name [,CONSTRAINED] )   
```  
  
## <a name="arguments"></a>引數  
 *Member_Name*  
 直接或間接指定成員的有效字串運算式。  
  
## <a name="remarks"></a>備註  
 **StrToMember**函式會傳回字串運算式中指定的成員。 **StrToMember**函式通常會搭配使用者自訂函數用來從外部函式中的成員規格傳回至 MDX 陳述式或 MDX 查詢參數化。  
  
-   使用 CONSTRAINED 旗標時，成員名稱必須可直接解析成合格的或不合格的成員名稱。 這個旗標用於降低遭到由指定字串發動資料隱碼攻擊的風險。 如果所提供的字串不能直接解析成限定或未限定成員名稱，會出現下列錯誤：「違反了 STRTOMEMBER 函數中 CONSTRAINED 旗標所加諸的限制。」  
  
-   沒有使用 CONSTRAINED 旗標時，指定的成員可以直接解析為成員名稱，或解析成會解析成名稱的 MDX 運算式。  
  
-   若要進一步了解集合和成員之間的差異，請參閱＜使用集合運算式＞和＜使用成員運算式＞。  
  
## <a name="examples"></a>範例  
 下列範例會傳回 Bayern 成員的 Reseller Sales Amount 量值中使用的 State-province 屬性階層**StrToMember**函式。 指定的字串提供了限定成員名稱。  
  
```  
SELECT {StrToMember ('[Geography].[State-Province].[Bayern]')}  
ON 0,  
{[Measures].[Reseller Sales Amount]} ON 1  
FROM [Adventure Works]  
  
```  
  
 下列範例會傳回使用 Bayern 成員的 Reseller Sales Amount 量值**StrToMember**函式。 因為成員名稱字串只提供不合格的成員名稱，所以查詢會傳回指定成員的第一個執行個體，這正好是在 Customer 維度的 Customer Geography 階層中，與 Reseller Sales 沒有交集。 最佳做法應規定指定合格的名稱，以確保預期的結果。  
  
```  
SELECT {StrToMember ('[Bayern]').Parent}  
ON 0,  
{[Measures].[Reseller Sales Amount]} ON 1  
FROM [Adventure Works]  
  
```  
  
 下列範例會傳回 Bayern 成員的 Reseller Sales Amount 量值中使用的 State-province 屬性階層**StrToMember**函式。 所提供的成員名稱字串會解析成合格的成員名稱。  
  
```  
SELECT {StrToMember('[Geography].[Geography].[Country].[Germany].FirstChild', CONSTRAINED)}  
ON 0,  
{[Measures].[Reseller Sales Amount]} ON 1  
FROM [Adventure Works]  
  
```  
  
 下列範例傳回因為 CONSTRAINED 旗標而發生的錯誤。 雖然所提供的成員名稱字串包含會解析成限定成員名稱的有效 MDX 成員運算式，但 CONSTRAINED 旗標要求成員名稱字串中包含限定或未限定成員名稱。  
  
```  
SELECT StrToMember ('[Geography].[Geography].[Country].[Germany].FirstChild', CONSTRAINED)  
ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 & #40;MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
