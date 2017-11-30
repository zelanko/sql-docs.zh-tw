---
title: "CALCULATE 陳述式 (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: CALCULATE
dev_langs: kbMDX
helpviewer_keywords: CALCULATE statement
ms.assetid: 41e196a1-d49e-487b-a42a-73e5d441ed1b
caps.latest.revision: "42"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: fe79fa5b94e07be72408fc72b0df6e57fa467ee2
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
---
# <a name="mdx-scripting---calculate"></a>MDX 指令碼-計算
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  以彙總值擴展 Cube 中的每個資料格。  
  
## <a name="syntax"></a>語法  
  
```  
  
CALCULATE  
```  
  
## <a name="arguments"></a>引數  
 無  
  
## <a name="remarks"></a>備註  
 當您使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 建立 Cube 時，CALCULATE 陳述式會自動包含在 Cube 的 MDX 指令碼中，做為第一個陳述式。 CALCULATE 陳述式會告知 Cube 中的每個資料格，從較低資料粒度的資料格彙總。 在彙總資料格之後，如果您隨後使用運算式擴展較低資料粒度的資料格，則會影響較高資料粒度資料格的彙總值。 大部分的狀況下，您可能希望發生此彙總，但您也可以移除它，或在這個陳述式前先執行其他陳述式。  
  
 CALCULATE 陳述式不能包含在 MDX 指令碼內的巢狀 Subcube。 使用 SCOPE 陳述式定義巢狀 Subcube。 如需有關 SCOPE 陳述式的詳細資訊，請參閱[SCOPE 陳述式 &#40;MDX &#41;](../mdx/mdx-scripting-scope.md).  
  
> [!NOTE]  
>  導出成員不會被彙總。  
  
## <a name="see-also"></a>請參閱  
 [MDX 指令碼陳述式 &#40;MDX &#41;](../mdx/mdx-scripting-statements-mdx.md)   
 [MDX 指令碼基礎觀念 &#40;Analysis Services &#41;](../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)   
 [定義指派和其他指令碼命令](../analysis-services/multidimensional-models/define-assignments-and-other-script-commands.md)  
  
  
