---
description: Ascendants (MDX)
title: 父 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: eb485e2785facba4a47647f8a51548e0140b3efb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491464"
---
# <a name="ascendants-mdx"></a>Ascendants (MDX)


  傳回指定成員的上階集合，包括該成員本身。  
  
## <a name="syntax"></a>語法  
  
```  
  
Ascendants(Member_Expression)  
```  
  
## <a name="arguments"></a>引數  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 **父**函式會將成員本身的所有上階從成員本身傳回至成員階層的最上層;更明確地說，它會針對指定的成員執行階層的後續順序遍歷，然後傳回所有與成員相關的上階成員，包括它本身在內的集合中。 這與 [祖系](../mdx/ancestor-mdx.md) 函數相反，後者會傳回特定層級的特定上階成員或上階。  
  
## <a name="examples"></a>範例  
 下列範例會傳回成員的轉銷商訂單計數 `[Sales Territory].[Northwest]` ，以及該成員的所有父項（來自「 **艾德作品** 」 cube）。 **祖先**函式會 `[Sales Territory].[Northwest]` 針對資料列軸的成員和其祖先結構來建立集合。  
  
```  
SELECT  
   Measures.[Reseller Order Count] ON COLUMNS,  
   Order(  
      Ascendants(  
         [Sales Territory].[Northwest]  
      ),  
      DESC  
   ) ON ROWS  
FROM  
   [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
