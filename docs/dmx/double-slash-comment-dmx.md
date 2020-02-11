---
title: 雙斜線（批註）（DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7f6e05ac728f6e1a9dda94dfcb07d26309b3e1f6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68061669"
---
# <a name="double-slash-comment-dmx"></a>雙斜線（批註）（DMX）
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  指出 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 不應執行的文字字串。 您可以在資料採礦延伸模組 (DMX) 陳述式內巢狀註解、在程式碼行的尾端包含註解，或者將註解插入單獨的一行。  
  
## <a name="syntax"></a>語法  
  
```  
  
// Comment_Text   
```  
  
#### <a name="parameters"></a>參數  
 *Comment_Text*  
 包含註解文字的字串。  
  
## <a name="remarks"></a>備註  
 // 只用於單行註解。 使用 // 插入的註解是以新行字元分隔。  
  
 註解沒有長度上限。  
  
 如需如何在 DMX 中使用不同類型批註的詳細資訊，請參閱[&#40;dmx&#41;的批註](../dmx/comments-dmx.md)。  
  
## <a name="see-also"></a>另請參閱  
 [斜線 &#40;批註&#41; &#40;DMX&#41;](../dmx/slash-star-comment-dmx.md)   
 [--&#40;批註&#41; &#40;DMX&#41; 摘要](../dmx/comment-dmx-summary.md)   
 [DMX&#41; Operator Reference &#40;的資料採礦延伸模組](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [DMX&#41;&#40;的運算子](../dmx/operators-dmx.md)  
  
  
