---
title: 斜線星形 （註解） (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1d96c65ea1dd187d5678987447415ca419ad10d7
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38020746"
---
# <a name="slash-star-comment-dmx"></a>斜線星形 （註解） (DMX)
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
 多行註解必須用 /* 和 \*/ 來表示。  
  
 註解沒有長度上限。  
  
 如需如何在 DMX 中使用不同類型的註解的詳細資訊，請參閱[註解&#40;DMX&#41;](../dmx/comments-dmx.md)。  
  
## <a name="see-also"></a>另請參閱  
 [雙斜線&#40;註解&#41; &#40;DMX&#41;](../dmx/double-slash-comment-dmx.md)   
 [-&#40;註解&#41; &#40;DMX&#41;摘要](../dmx/comment-dmx-summary.md)   
 [資料採礦延伸模組&#40;DMX&#41;運算子參考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [運算子&#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
