---
title: 詞彙擷取轉換編輯器 （進階索引標籤） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.termextraction.advanced.f1
helpviewer_keywords:
- Term Extraction Transformation Editor
ms.assetid: 87118281-6e3c-499e-bac4-fa4c24bb12c6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ea6582aacefc7c17450e59689bec29c260a38d07
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2019
ms.locfileid: "58385036"
---
# <a name="term-extraction-transformation-editor-advanced-tab"></a>詞彙擷取轉換編輯器 (進階索引標籤)
  使用 [詞彙擷取轉換編輯器] 對話方塊的 [進階] 索引標籤，即可指定擷取的屬性，例如頻率、長度和是否擷取單字或片語。  
  
 若要深入了解詞彙擷取轉換，請參閱＜ [Term Extraction Transformation](data-flow/transformations/term-extraction-transformation.md)＞。  
  
## <a name="options"></a>選項。  
 **名詞**  
 指定轉換只擷取個別的名詞。  
  
 **名詞片語**  
 指定轉換只擷取名詞片語。  
  
 **名詞和名詞片語**  
 指定轉換同時擷取名詞和名詞片語。  
  
 **頻率**  
 指定分數是詞彙的頻率。  
  
 **TFIDF**  
 指定分數是詞彙的 TFIDF 值。 TFIDF 分數是詞彙頻率 」 和 「 反向文件頻率，定義為乘積：詞彙 T 的 TFIDF = （T 的頻率） * log ((輸入中的 #rows) / （#rows T）)  
  
 **頻率臨界值**  
 指定擷取單字或片語前，該單字或片語必須出現的次數。 預設值為 2。  
  
 **詞彙最大長度**  
 指定在文字中，片語的最大長度。 此選項只會影響名詞片語。 預設值為 12。  
  
 **使用區分大小寫的詞彙擷取**  
 指定擷取是否區分大小寫。 預設為 `False`。  
  
 **設定錯誤輸出**  
 使用 [[設定錯誤輸出]](../../2014/integration-services/configure-error-output.md) 對話方塊，即可指定造成錯誤之資料列的錯誤處理。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [詞彙擷取轉換編輯器 &#40;詞彙擷取索引標籤&#41;](../../2014/integration-services/term-extraction-transformation-editor-term-extraction-tab.md)   
 [詞彙擷取轉換編輯器 &#40;排除索引標籤&#41;](../../2014/integration-services/term-extraction-transformation-editor-exclusion-tab.md)   
 [詞彙查閱轉換](data-flow/transformations/lookup-transformation.md)  
  
  
