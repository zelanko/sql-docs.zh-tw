---
title: "雙斜線 （註解） (DMX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: DMX
helpviewer_keywords:
- double forward slashes
- commenting characters
- // (comment)
ms.assetid: c2ab9ca1-9fc9-4162-97f9-a9433d189220
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 408486f48e978f036ef249cbe4909e58f6f4dfa9
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="double-slash-comment-dmx"></a>雙斜線 （註解） (DMX)
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
  
 如需如何在 DMX 中使用不同類型的註解的詳細資訊，請參閱[註解 &#40; DMX &#41;](../dmx/comments-dmx.md)。  
  
## <a name="see-also"></a>請參閱＜  
 [斜線星狀 &#40;註解 &#41;&#40; DMX &#41;](../dmx/slash-star-comment-dmx.md)   
 [-&#40;註解 &#41;&#40; DMX &#41;摘要](../dmx/comment-dmx-summary.md)   
 [資料採礦延伸模組 &#40; DMX &#41;運算子參考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [運算子 &#40; DMX &#41;](../dmx/operators-dmx.md)  
  
  
