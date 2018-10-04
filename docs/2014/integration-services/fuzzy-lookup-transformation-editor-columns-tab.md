---
title: 模糊查閱轉換編輯器 （資料行索引標籤） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.fuzzylookuptransformation.columns.f1
helpviewer_keywords:
- Fuzzy Lookup Transformation Editor
ms.assetid: aaf45327-79e9-4760-9b4d-546ace91b5b4
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 36c8feb7105af5b6f38b53be9e40f5ca28e752ba
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48071358"
---
# <a name="fuzzy-lookup-transformation-editor-columns-tab"></a>模糊查閱轉換編輯器 (資料行索引標籤)
  使用 **[模糊查閱轉換編輯器]** 對話方塊的 **[資料行]** 索引標籤，即可設定輸入與輸出資料行的屬性。  
  
 若要深入了解模糊查閱轉換，請參閱＜ [Fuzzy Lookup Transformation](data-flow/transformations/lookup-transformation.md)＞。  
  
## <a name="options"></a>選項。  
 **可用的輸入資料行**  
 拖曳輸入資料行，即可將資料行連接到可用的查閱資料行。 這些資料行必須擁有相符的、支援的資料類型。 在 [ [建立關聯性](data-flow/transformations/create-relationships.md) ] 對話方塊中選取對應行，並以滑鼠右鍵按一下來編輯對應。  
  
 **名稱**  
 檢視可用輸入資料行的名稱。  
  
 **通過**  
 指定是否在轉換的輸出中包含輸入資料行。  
  
 **可用的查閱資料行**  
 使用核取方塊即可選取要執行模糊查閱作業的資料行。  
  
 **查閱資料行**  
 從可用的參考資料表資料行清單中選取查閱資料行。 您的選取項目會反映在 **[可用的查閱資料行]** 資料表的核取方塊選取項目中。 選取 **[可用的查閱資料行]** 資料表中的資料行會建立輸出資料行，其中包含傳回的每個相符資料列的參考資料表資料行值。  
  
 **輸出別名**  
 輸入每個查閱資料行之輸出的別名。 預設值為附加數值索引值之查閱資料行的名稱；不過，您也可以選擇任何唯一的、描述性名稱。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [模糊查閱轉換編輯器&#40;參考資料表索引標籤&#41;](../../2014/integration-services/fuzzy-lookup-transformation-editor-reference-table-tab.md)   
 [模糊查閱轉換編輯器&#40;進階索引標籤&#41;](../../2014/integration-services/fuzzy-lookup-transformation-editor-advanced-tab.md)  
  
  
