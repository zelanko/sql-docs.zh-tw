---
title: "詞彙擷取轉換編輯器 （進階索引標籤） |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.termextraction.advanced.f1
helpviewer_keywords:
- Term Extraction Transformation Editor
ms.assetid: 87118281-6e3c-499e-bac4-fa4c24bb12c6
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 605085b59357a98011c801f8aa4675e89c3cd8a9
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="term-extraction-transformation-editor-advanced-tab"></a>詞彙擷取轉換編輯器 (進階索引標籤)
  使用 [詞彙擷取轉換編輯器] 對話方塊的 [進階] 索引標籤，即可指定擷取的屬性，例如頻率、長度和是否擷取單字或片語。  
  
 若要深入了解詞彙擷取轉換，請參閱＜ [Term Extraction Transformation](../../../integration-services/data-flow/transformations/term-extraction-transformation.md)＞。  
  
## <a name="options"></a>選項  
 **名詞**  
 指定轉換只擷取個別的名詞。  
  
 **名詞片語**  
 指定轉換只擷取名詞片語。  
  
 **名詞和名詞片語**  
 指定轉換同時擷取名詞和名詞片語。  
  
 **頻率**  
 指定分數是詞彙的頻率。  
  
 **TFIDF**  
 指定分數是詞彙的 TFIDF 值。 TFIDF 分數是「詞彙頻率」和「反向文件頻率」的乘積，定義為︰詞彙 T 的 TFIDF = (T 的頻率) * log((輸入中的資料列數) / (具有 T 的資料列數))  
  
 **頻率臨界值**  
 指定擷取單字或片語前，該單字或片語必須出現的次數。 預設值為 2。  
  
 **詞彙最大長度**  
 指定在文字中，片語的最大長度。 此選項只會影響名詞片語。 預設值為 12。  
  
 **使用區分大小寫的詞彙擷取**  
 指定擷取是否區分大小寫。 預設值為 **False**。  
  
 **設定錯誤輸出**  
 使用 [設定錯誤輸出](http://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) 對話方塊，即可指定造成錯誤之資料列的錯誤處理。  
  
## <a name="see-also"></a>請參閱＜  
 [Integration Services 錯誤和訊息參考](../../../integration-services/integration-services-error-and-message-reference.md)   
 [詞彙擷取轉換編輯器 &#40;詞彙擷取 索引標籤&#41;](../../../integration-services/data-flow/transformations/term-extraction-transformation-editor-term-extraction-tab.md)   
 [詞彙擷取轉換編輯器 &#40;排除索引標籤 &#41;](../../../integration-services/data-flow/transformations/term-extraction-transformation-editor-exclusion-tab.md)   
 [詞彙查閱轉換](../../../integration-services/data-flow/transformations/term-lookup-transformation.md)  
  
  
