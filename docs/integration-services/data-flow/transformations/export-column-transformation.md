---
title: "匯出資料行轉換 |Microsoft 文件"
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
- sql13.dts.designer.exportcolumntrans.f1
helpviewer_keywords:
- exporting data
- append options [Integration Services]
- Export Column transformation [Integration Services]
- columns [Integration Services], exporting
- inserting data
- truncate options [Integration Services]
ms.assetid: 678d2dfc-e40c-4fbb-b2cc-42fffc44478a
caps.latest.revision: 45
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e7e611452f931d049c63c822587dc7610bf1eb25
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="export-column-transformation"></a>匯出資料行轉換
  「匯出資料行」轉換會讀取資料流程中的資料，並將資料插入檔案中。 例如，如果資料流程包含產品資訊 (例如每一項產品的圖片)，則可使用「匯出資料行」轉換將影像儲存到檔案中。  
  
## <a name="append-and-truncate-options"></a>附加和截斷選項  
 下表說明附加和截斷選項的設定影響結果的方式。  
  
|附加|截斷|檔案存在|結果|  
|------------|--------------|-----------------|-------------|  
|False|False|否|轉換會建立新檔案，並將資料寫入檔案。|  
|True|False|否|轉換會建立新檔案，並將資料寫入檔案。|  
|False|True|否|轉換會建立新檔案，並將資料寫入檔案。|  
|True|True|否|轉換未通過設計階段驗證。 將兩個屬性都設定為 [true] 是無效的。|  
|False|False|是|發生執行階段錯誤。 檔案存在，但轉換無法寫入該檔案。|  
|False|True|是|轉換會刪除並重新建立檔案，然後將資料寫入該檔案中。|  
|True|False|是|轉換會開啟該檔案，並將資料寫入檔案結尾。|  
|True|True|是|轉換未通過設計階段驗證。 將兩個屬性都設定為 [true] 是無效的。|  
  
## <a name="configuration-of-the-export-column-transformation"></a>設定匯出資料行轉換  
 您可以利用下列方式設定「匯出資料行」轉換：  
  
-   指定資料的資料行，以及包含要寫入資料的檔案路徑的資料行。  
  
-   指定資料插入作業應附加或截斷現有檔案。  
  
-   指定是否要將位元組順序標記 (BOM) 寫入該檔案。  
  
    > [!NOTE]  
    >  BOM 只有在資料未附加至現有檔案，且資料類型為 DT_NTEXT 時才寫入。  
  
 轉換使用成對的輸入資料行：一個資料行包含一個檔案名稱，另一個資料行則包含資料。 資料集中的每一個資料列都可指定不同的檔案。 當轉換處理資料列時，會將資料插入指定的檔案中。 在執行階段，轉換會建立檔案 (如果檔案不存在)，然後將資料寫入這些檔案中。 要寫入的資料的資料類型必須為 DT_TEXT、DT_NTEXT 或 DT_IMAGE。 如需詳細資訊，請參閱＜ [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md)＞。  
  
 這個轉換有一個輸入、一個輸出與一個錯誤輸出。  
  
 您可以透過「 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師」或以程式設計方式設定屬性。  
  
 如需可在 [匯出資料行轉換編輯器] 對話方塊中設定之屬性的詳細資訊，請參閱[匯出資料行轉換編輯器 &#40;資料行頁面&#41;](../../../integration-services/data-flow/transformations/export-column-transformation-editor-columns-page.md)。  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [通用屬性](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [轉換自訂屬性](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 如需如何設定屬性的詳細資訊，請參閱 [設定資料流程元件的屬性](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)。  
  
  
