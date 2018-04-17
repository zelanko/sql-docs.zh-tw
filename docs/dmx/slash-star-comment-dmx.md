---
title: Star （註解） (DMX) 的斜線 |Microsoft 文件
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- commenting characters
- forward slash-asterisk character pairs
- /*...*/ (comment)
ms.assetid: 163976cc-aa47-4eda-bd98-03c1a397f80e
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 900b602a00e11cc58cd6500cafc99eb90dcca62d
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="slash-star-comment-dmx"></a>斜線星狀 （註解） (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  指出 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 不應執行的文字字串。 伺服器不會評估註解字元之間的文字 / * 和\*/。 您可以在資料採礦延伸模組 (DMX) 陳述式內巢狀註解、在程式碼行的尾端包含註解，或者將註解插入單獨的一行。  
  
## <a name="syntax"></a>語法  
  
```  
  
/* Comment_Text */  
```  
  
#### <a name="parameters"></a>參數  
 *Comment_Text*  
 包含註解文字的字串。  
  
## <a name="remarks"></a>備註  
 多行註解必須以 / * 和\*/。  
  
 註解沒有長度上限。  
  
 如需如何在 DMX 中使用不同類型的註解的詳細資訊，請參閱[註解 &#40; DMX &#41;](../dmx/comments-dmx.md)。  
  
## <a name="see-also"></a>請參閱  
 [雙斜線 &#40;註解 &#41;&#40; DMX &#41;](../dmx/double-slash-comment-dmx.md)   
 [-&#40;註解 &#41;&#40; DMX &#41;摘要](../dmx/comment-dmx-summary.md)   
 [資料採礦延伸模組 &#40; DMX &#41;運算子參考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [運算子 &#40; DMX &#41;](../dmx/operators-dmx.md)  
  
  
