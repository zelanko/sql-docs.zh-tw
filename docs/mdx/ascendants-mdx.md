---
title: 祖先（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 16c6f812d1d7cae5a81a8e64fb425f4d33f4cb5c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68017066"
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
 祖**函數會將成員**的所有上階從成員本身傳回至成員階層的最上層;更具體來說，它會針對指定的成員執行階層的後序遍歷，然後在集合中傳回與該成員相關的所有上階成員，包括其本身。 這[與上階函數相反](../mdx/ancestor-mdx.md)，後者會在特定層級傳回特定的上階成員或上階。  
  
## <a name="examples"></a>範例  
 下列範例會傳回`[Sales Territory].[Northwest]`成員的轉售商訂單計數，以及該成員在「**艾德作品**」 cube 中的所有祖先。 **祖先**函數會針對資料列軸，建立`[Sales Territory].[Northwest]`包含成員和其祖先的集合。  
  
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
  
  
