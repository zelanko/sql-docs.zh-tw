---
title: 詞彙查閱轉換編輯器 （詞彙查閱索引標籤） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.termlookup.termlookup.f1
helpviewer_keywords:
- Term Lookup Transformation Editor
ms.assetid: 245d3466-d51f-4073-978a-694a8d9dfaec
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2939d160773d60944a2e8a786e5495cea366edb1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66055126"
---
# <a name="term-lookup-transformation-editor-term-lookup-tab"></a>詞彙查閱轉換編輯器 (詞彙查閱索引標籤)
  使用 **[詞彙查閱轉換編輯器]** 對話方塊的 **[詞彙查閱]** 索引標籤，即可將輸入資料行對應至參考資料表的查閱資料行，並提供每一個輸出資料行的別名。  
  
 若要深入了解模糊查閱轉換，請參閱＜ [Term Lookup Transformation](data-flow/transformations/lookup-transformation.md)＞。  
  
## <a name="options"></a>選項  
 **可用的輸入資料行**  
 使用核取方塊選取輸入資料行，即可讓這些輸入資料行在不變更的狀況下通過至輸出。 將輸入資料行拖曳至 **[可用的參考資料行]** 清單，即可對應至參考資料表的查閱資料行。 輸入和查閱資料行都必須有相符、受支援的資料類型，包括 DT_NTEXT 或 DT_WSTR。 在 [ [建立關聯性](data-flow/transformations/create-relationships.md) ] 對話方塊中選取對應行，並以滑鼠右鍵按一下來編輯對應。  
  
 **[可用的參考資料行]**  
 檢視參考資料表中可用的資料行。 選擇包含要比對之詞彙清單的資料行。  
  
 **通過資料行**  
 從可用的輸入資料行清單中選取。 您的選擇會反映在 **[可用的輸入資料行]** 資料表的核取方塊選擇中。  
  
 **輸出資料行別名**  
 輸入每一個輸出資料行的別名。 預設為資料行的名稱；不過，您可以選擇任何唯一的描述性名稱。  
  
 **設定錯誤輸出**  
 使用 [ [設定錯誤輸出](../../2014/integration-services/configure-error-output.md) ] 對話方塊，即可指定造成錯誤之資料列的錯誤處理選項。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [詞彙查閱轉換編輯器 &#40;參考資料表索引標籤&#41;](../../2014/integration-services/term-lookup-transformation-editor-reference-table-tab.md)   
 [詞彙查閱轉換編輯器 &#40;進階索引標籤&#41;](../../2014/integration-services/term-lookup-transformation-editor-advanced-tab.md)   
 [詞彙擷取轉換](data-flow/transformations/term-extraction-transformation.md)  
  
  
