---
title: "匯出資料行轉換編輯器 （資料行頁面） |Microsoft 文件"
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
- sql13.dts.designer.fileextractortransformation.columns.f1
helpviewer_keywords:
- Export Column Transformation Editor
ms.assetid: b659a5c2-5509-4b5b-9c82-136c971d5c7f
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e3538e9379c48faaa700f56aa1ecf0ceafc68e2a
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="export-column-transformation-editor-columns-page"></a>匯出資料行轉換編輯器 (資料行頁面)
  使用 **[匯出資料行轉換編輯器]** 對話方塊的 **[資料行]** 頁面，即可指定資料流程中要擷取至檔案的資料行。 您可以指定匯出資料行轉換將資料附加至檔案或複寫現有的檔案。  
  
 若要深入了解匯出資料行轉換，請參閱＜ [Export Column Transformation](../../../integration-services/data-flow/transformations/export-column-transformation.md)＞。  
  
## <a name="options"></a>選項。  
 **擷取資料行**  
 從包含文字或影像資料的輸入資料行清單中選取。 所有資料列應有 **[擷取資料行]** 和 **[檔案路徑資料行]**的定義。  
  
 **[檔案路徑資料行]**  
 從包含檔案路徑和檔案名稱的輸入資料行清單中選取。 所有資料列應有 **[擷取資料行]** 和 **[檔案路徑資料行]**的定義。  
  
 **允許附加**  
 指定轉換是否將資料附加至現有的檔案。 預設值為 **false**。  
  
 **強制截斷**  
 指定轉換是否在寫入資料之前刪除現有檔案的內容。 預設值為 **false**。  
  
 **寫入 BOM**  
 指定是否將位元組順序標記 (BOM) 寫入檔案。 當資料擁有 **DT_NTEXT** 或 DT_WSTR 資料類型，且未附加至現有的資料檔案時，才會寫入 BOM。  
  
## <a name="see-also"></a>請參閱＜  
 [Integration Services 錯誤和訊息參考](../../../integration-services/integration-services-error-and-message-reference.md)   
 [匯出資料行轉換編輯器 & #40;錯誤輸出頁面 & #41;](../../../integration-services/data-flow/transformations/export-column-transformation-editor-error-output-page.md)  
  
  
