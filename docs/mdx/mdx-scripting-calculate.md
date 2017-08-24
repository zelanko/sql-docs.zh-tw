---
title: "CALCULATE 陳述式 (MDX) |Microsoft 文件"
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
- CALCULATE
dev_langs:
- kbMDX
helpviewer_keywords:
- CALCULATE statement
ms.assetid: 41e196a1-d49e-487b-a42a-73e5d441ed1b
caps.latest.revision: 42
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: d8e74fd0cd09e050c11d2eb403d31527402f008b
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="mdx-scripting---calculate"></a>MDX 指令碼-計算
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
## <a name="see-also"></a>另請參閱  
 [MDX 指令碼陳述式 &#40;MDX &#41;](../mdx/mdx-scripting-statements-mdx.md)   
 [MDX 指令碼基礎觀念 &#40;Analysis Services &#41;](../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)   
 [定義指派和其他指令碼命令](../analysis-services/multidimensional-models/define-assignments-and-other-script-commands.md)  
  
  

