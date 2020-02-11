---
title: --（批註）（DMX）摘要 |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 241ab17847a040e33c1fdb5e116e39fbc535d16d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68073093"
---
# <a name="---comment-dmx-summary"></a>--（批註）（DMX）摘要
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  指出 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 不應執行的文字字串。 您可以在資料採礦延伸模組 (DMX) 陳述式內巢狀註解、在程式碼行的尾端包含註解，或者將註解插入單獨的一行。  
  
## <a name="syntax"></a>語法  
  
```  
  
-- Comment_Text      
```  
  
#### <a name="parameters"></a>參數  
 *Comment_Text*  
 包含註解文字的字串。  
  
## <a name="remarks"></a>備註  
 在單行或巢狀註解使用這個運算子。 使用 -- 插入的註解會使用新行字元分隔。  
  
 註解沒有長度上限。  
  
 如需如何在 DMX 中使用不同類型批註的詳細資訊，請參閱[&#40;dmx&#41;的批註](../dmx/comments-dmx.md)。  
  
## <a name="see-also"></a>另請參閱  
 [斜線 &#40;批註&#41; &#40;DMX&#41;](../dmx/slash-star-comment-dmx.md)   
 [&#40;批註&#41; &#40;DMX&#41;的雙斜線](../dmx/double-slash-comment-dmx.md)   
 [DMX&#41; Operator Reference &#40;的資料採礦延伸模組](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [DMX&#41;&#40;的運算子](../dmx/operators-dmx.md)  
  
  
