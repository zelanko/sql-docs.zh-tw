---
title: 匯入資料行轉換 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.importcolumntrans.f1
helpviewer_keywords:
- Import Column transformation [Integration Services]
- columns [Integration Services], importing
- importing data, SSIS packages
- inserting data
ms.assetid: ac3b74c1-ef54-4297-8062-1734324fffcc
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a51ed134b1cac2c6282b8bb2566dc9d27873bc05
ms.sourcegitcommit: 0638b228980998de9056b177c83ed14494b9ad74
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/14/2018
ms.locfileid: "51642015"
---
# <a name="import-column-transformation"></a>匯入資料行轉換
  「匯入資料行」轉換會從檔案讀取資料，並將資料加入至資料流程中的資料行。 封裝可使用此轉換將其他檔案中儲存的文字和影像加入至資料流程。 例如，將資料載入儲存產品資訊之資料表中的資料流程，即可加入「匯入資料行」轉換，以便從檔案匯入客戶對每項產品的檢閱，然後將檢閱加入至資料流程。  
  
 您可以利用下列方式設定「匯入資料行」轉換：  
  
-   指定轉換要加入資料的資料行。  
  
-   指定轉換是否需要位元組順序標示 (BOM)。  
  
    > [!NOTE]  
    >  BOM 只有在資料的資料類型為 DT_NTEXT 時才需要。  
  
 轉換輸入中的資料行包含擁有該資料的檔案名稱。 資料集中的每一個資料列都可指定不同的檔案。 當「匯入資料行」轉換處理某一個資料列時，會讀取檔名、開啟檔案系統中對應的檔案，以及將檔案內容載入輸出資料行。 輸出資料行的資料類型必須為 DT_TEXT、DT_NTEXT 或 DT_IMAGE。 如需詳細資訊，請參閱 [Integration Services 資料類型](../../../integration-services/data-flow/integration-services-data-types.md)。  
  
 這個轉換有一個輸入、一個輸出與一個錯誤輸出。  
  
## <a name="configuration-of-the-import-column-transformation"></a>匯入資料行轉換的組態  
 您可以透過 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [通用屬性](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [轉換自訂屬性](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>相關工作  
 如需如何設定此元件屬性的資訊，請參閱 [設定資料流程元件的屬性](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="see-also"></a>另請參閱  
 [匯出資料行轉換](../../../integration-services/data-flow/transformations/export-column-transformation.md)   
 [資料流程](../../../integration-services/data-flow/data-flow.md)   
 [Integration Services 轉換](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
