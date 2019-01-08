---
title: 上階 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3122b3aa2f53da69f88e6ffad508f12c8e10da1c
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2018
ms.locfileid: "52404343"
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
 **上階**函式會傳回成員的祖系的所有成員本身的成員之階層最上方; 更具體來說，它會執行後序走訪，階層的指定的成員，然後傳回與成員，包括本身，在一組相關的所有上階成員。 這是相對於[祖系](../mdx/ancestor-mdx.md)函式會傳回特定的上階成員或上的階，在特定層級。  
  
## <a name="examples"></a>範例  
 下列範例會傳回的轉售商訂單計數`[Sales Territory].[Northwest]`成員以及從該成員的所有上階**Adventure Works** cube。 **上階**函式會建構集合，包括`[Sales Territory].[Northwest]`成員，而且它在 ROWS 軸的上階。  
  
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
  
  
