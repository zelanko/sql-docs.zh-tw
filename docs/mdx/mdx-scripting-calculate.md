---
description: CALCULATE 陳述式 (MDX)
title: 計算 (MDX) 的語句 |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ff995f08ffef27abca65db10ff2cd38f2dd01e95
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196962"
---
# <a name="mdx-scripting---calculate"></a>MDX 指令碼 - CALCULATE


  以彙總值擴展 Cube 中的每個資料格。  
  
## <a name="syntax"></a>語法  
  
```  
  
CALCULATE  
```  
  
## <a name="arguments"></a>引數  
 無  
  
## <a name="remarks"></a>備註  
 當您使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 建立 Cube 時，CALCULATE 陳述式會自動包含在 Cube 的 MDX 指令碼中，做為第一個陳述式。 CALCULATE 陳述式會告知 Cube 中的每個資料格，從較低資料粒度的資料格彙總。 在彙總資料格之後，如果您隨後使用運算式擴展較低資料粒度的資料格，則會影響較高資料粒度資料格的彙總值。 大部分的狀況下，您可能希望發生此彙總，但您也可以移除它，或在這個陳述式前先執行其他陳述式。  
  
 CALCULATE 陳述式不能包含在 MDX 指令碼內的巢狀 Subcube。 使用 SCOPE 陳述式定義巢狀 Subcube。 如需 SCOPE 語句的詳細資訊，請參閱 [Scope 語句 &#40;MDX&#41;](../mdx/mdx-scripting-scope.md)。  
  
> [!NOTE]  
>  導出成員不會被彙總。  
  
## <a name="see-also"></a>另請參閱  
 [Mdx 腳本語句 &#40;MDX&#41;](../mdx/mdx-scripting-statements-mdx.md)   
 [MDX 腳本基礎 &#40;Analysis Services&#41;](/analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services)   
 [定義指派和其他指令碼命令](/analysis-services/multidimensional-models/define-assignments-and-other-script-commands)  
  
