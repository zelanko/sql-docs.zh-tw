---
title: 匯入資料行轉換 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.importcolumntrans.f1
helpviewer_keywords:
- Import Column transformation [Integration Services]
- columns [Integration Services], importing
- importing data, SSIS packages
- inserting data
ms.assetid: ac3b74c1-ef54-4297-8062-1734324fffcc
author: janinezhang
ms.author: janinez
ms.openlocfilehash: a32aedee115fc828d1109f2a8620ca7a81eb704d
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84939484"
---
# <a name="import-column-transformation"></a>匯入資料行轉換
  「匯入資料行」轉換會從檔案讀取資料，並將資料加入至資料流程中的資料行。 封裝可使用此轉換將其他檔案中儲存的文字和影像加入至資料流程。 例如，將資料載入儲存產品資訊之資料表中的資料流程，即可加入「匯入資料行」轉換，以便從檔案匯入客戶對每項產品的檢閱，然後將檢閱加入至資料流程。  
  
 您可以利用下列方式設定「匯入資料行」轉換：  
  
-   指定轉換要加入資料的資料行。  
  
-   指定轉換是否需要位元組順序標示 (BOM)。  
  
    > [!NOTE]  
    >  BOM 只有在資料的資料類型為 DT_NTEXT 時才需要。  
  
 轉換輸入中的資料行包含擁有該資料的檔案名稱。 資料集中的每一個資料列都可指定不同的檔案。 當「匯入資料行」轉換處理某一個資料列時，會讀取檔名、開啟檔案系統中對應的檔案，以及將檔案內容載入輸出資料行。 輸出資料行的資料類型必須為 DT_TEXT、DT_NTEXT 或 DT_IMAGE。 如需詳細資訊，請參閱 [Integration Services 資料類型](../integration-services-data-types.md)。  
  
 這個轉換有一個輸入、一個輸出與一個錯誤輸出。  
  
## <a name="configuration-of-the-import-column-transformation"></a>匯入資料行轉換的組態  
 您可以透過 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [Common Properties](../../common-properties.md)  
  
-   [轉換自訂屬性](transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>相關工作  
 如需如何設定此元件屬性的資訊，請參閱 [設定資料流程元件的屬性](../set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="see-also"></a>另請參閱  
 [匯出資料行轉換](export-column-transformation.md)   
 [資料流程](../data-flow.md)   
 [Integration Services 轉換](integration-services-transformations.md)  
  
  
