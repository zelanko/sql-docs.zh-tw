---
title: 匯出資料行轉換編輯器 （資料行頁面） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.fileextractortransformation.columns.f1
helpviewer_keywords:
- Export Column Transformation Editor
ms.assetid: b659a5c2-5509-4b5b-9c82-136c971d5c7f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d7682e3c22885b50e1516a8f30cce468852ae2c7
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2019
ms.locfileid: "58378056"
---
# <a name="export-column-transformation-editor-columns-page"></a>匯出資料行轉換編輯器 (資料行頁面)
  使用 **[匯出資料行轉換編輯器]** 對話方塊的 **[資料行]** 頁面，即可指定資料流程中要擷取至檔案的資料行。 您可以指定匯出資料行轉換將資料附加至檔案或複寫現有的檔案。  
  
 若要深入了解匯出資料行轉換，請參閱＜ [Export Column Transformation](data-flow/transformations/export-column-transformation.md)＞。  
  
## <a name="options"></a>選項。  
 **擷取資料行**  
 從包含文字或影像資料的輸入資料行清單中選取。 所有資料列應有 **[擷取資料行]** 和 **[檔案路徑資料行]** 的定義。  
  
 **[檔案路徑資料行]**  
 從包含檔案路徑和檔案名稱的輸入資料行清單中選取。 所有資料列應有 **[擷取資料行]** 和 **[檔案路徑資料行]** 的定義。  
  
 **允許附加**  
 指定轉換是否將資料附加至現有的檔案。 預設為 `false`。  
  
 **強制截斷**  
 指定轉換是否在寫入資料之前刪除現有檔案的內容。 預設為 `false`。  
  
 **寫入 BOM**  
 指定是否將位元組順序標記 (BOM) 寫入檔案。 當資料擁有 `DT_NTEXT` 或 DT_WSTR 資料類型，且未附加至現有的資料檔時，才會寫入 BOM。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [匯出資料行轉換編輯器 &#40;錯誤輸出頁面&#41;](../../2014/integration-services/export-column-transformation-editor-error-output-page.md)  
  
  
