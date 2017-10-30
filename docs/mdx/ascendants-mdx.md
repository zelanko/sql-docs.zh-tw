---
title: "上階 (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ASCENDANTS
dev_langs:
- kbMDX
helpviewer_keywords:
- Ascendants function
ms.assetid: a2baf4a2-7d66-4766-b708-739a3c21b09e
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: a290643abeb55db3a2c7091976731af9dbb200ff
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="ascendants-mdx"></a>Ascendants (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

