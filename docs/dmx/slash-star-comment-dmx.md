---
title: 斜線星號（批註）（DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f09533b68ab6dc3c771a09b70faf71087ed69a62
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2020
ms.locfileid: "86970399"
---
# <a name="slash-star-comment-dmx"></a>斜線星號（批註）（DMX）
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  指出 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 不應執行的文字字串。 伺服器不會評估批註字元/* 和/之間的文字 \* 。 您可以在資料採礦延伸模組 (DMX) 陳述式內巢狀註解、在程式碼行的尾端包含註解，或者將註解插入單獨的一行。  
  
## <a name="syntax"></a>語法  
  
```  
  
/* Comment_Text */  
```  
  
#### <a name="parameters"></a>參數  
 *Comment_Text*  
 包含註解文字的字串。  
  
## <a name="remarks"></a>備註  
 多行註解必須用 /* 和 \*/ 來表示。  
  
 註解沒有長度上限。  
  
 如需如何在 DMX 中使用不同類型批註的詳細資訊，請參閱[&#40;dmx&#41;的批註](../dmx/comments-dmx.md)。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;批註&#41; &#40;DMX&#41;的雙斜線](../dmx/double-slash-comment-dmx.md)   
 [--&#40;批註&#41; &#40;DMX&#41; 摘要](../dmx/comment-dmx-summary.md)   
 [DMX&#41; Operator Reference &#40;的資料採礦延伸模組](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [DMX&#41;&#40;的運算子](../dmx/operators-dmx.md)  
  
  
