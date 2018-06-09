---
title: 上階 (MDX) |Microsoft 文件
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1ef9cccb488cebb08c1b9721c40cb8037ea8687a
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2018
ms.locfileid: "34739617"
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
 **上階**函式會傳回所有成員的上階成員本身的成員之階層最上方; 更明確地說，它會執行指定的成員的階層後序走訪和則傳回所有上階成員與相關的成員，包括它自己，集合中。 這是相對於[祖系](../mdx/ancestor-mdx.md)函式會傳回特定的上階成員或上的階，在特定層級。  
  
## <a name="examples"></a>範例  
 下列範例會傳回的轉售商訂單計數`[Sales Territory].[Northwest]`成員，並從該成員的所有上階**Adventure Works** cube。 **上階**函式建構一個集合，包含`[Sales Territory].[Northwest]`成員和其資料列軸的上階。  
  
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
 [MDX 函數參考&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
