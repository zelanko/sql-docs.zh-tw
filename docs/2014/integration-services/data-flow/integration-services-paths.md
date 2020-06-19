---
title: Integration Services 路徑 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- paths [Integration Services], about paths
- data flow [Integration Services], paths
- paths [Integration Services]
- destinations [Integration Services], paths
- sources [Integration Services], paths
ms.assetid: 6c4629a9-2ede-4011-9101-3b342249640e
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 06746ae92c4e5d868cf5aff709ceccbbd200b68e
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84915442"
---
# <a name="integration-services-paths"></a>Integration Services 路徑
  將一個資料流程元件的輸出與另一元件的輸入連接，路徑可連接資料流程中的兩個元件。 路徑具有一個來源和一個目的地。 例如，如果路徑連接 OLE DB 來源和「排序」轉換，則 OLE DB 來源是路徑的來源，而「排序」轉換是路徑的目的地。 來源是路徑開始處的元件，而目的地是路徑結束處的元件。  
  
 如果您在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中執行封裝，則可將資料檢視器附加到路徑，來檢視資料流程中的資料。 資料檢視器可以設定為在方格中顯示資料。 資料檢視器是一種有用的偵錯工具。 如需詳細資訊，請參閱 [偵錯資料流程](../troubleshooting/debugging-data-flow.md)。  
  
## <a name="configuration-of-the-path"></a>設定路徑  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師提供 [資料流程路徑編輯器]  對話方塊，用以設定路徑屬性、檢視通過該路徑之資料行的中繼資料，並設定資料檢視器。  
  
 可設定的路徑屬性包括名稱、描述及路徑的註解。 您還可以程式設計方式設定路徑。 如需詳細資訊，請參閱 [以程式設計方式連接資料流程元件](../building-packages-programmatically/connecting-data-flow-components-programmatically.md)。  
  
 路徑註解顯示路徑來源的名稱，或在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中 [資料流程] 索引標籤設計介面上的路徑名稱。 路徑註解與您可加入資料流程、控制流程和事件處理常式的註解相似。 唯一不同之處在於路徑註解是附加到路徑上的，而其他註解則顯示於 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師的 [資料流程]、[控制流程] 和 [事件處理常式] 索引標籤上。  
  
 中繼資料顯示上一個元件輸出中之每個資料行的名稱、資料類型、有效位數、小數位數、長度、字碼頁和來源元件。 來源元件是建立資料行的資料流程元件。 但不一定是資料流程中的第一個元件。 例如，「聯集全部」和「排序」轉換都會建立自己的資料行，因此它們是其輸出資料行的來源。 相反地，「複製資料行」轉換可以通過資料行而不對其進行變更，或可以藉由複製輸入資料行來建立新的資料行。 因此「複製資料行」轉換僅是新資料行的來源元件。  
  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需可在 [資料流程路徑編輯器]**** 對話方塊中設定之屬性的詳細資訊，請按一下下列其中一個主題：  
  
-   [[資料流程路徑編輯器] &#40;一般頁面&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [資料流程路徑編輯器 &#40;中繼資料頁面&#41;](../data-flow-path-editor-metadata-page.md)  
  
-   [資料檢視器頁面 &#40;的資料流程路徑編輯器&#41;](../data-flow-path-editor-data-viewers-page.md)  
  
 如需可透過程式設計方式設定之屬性的詳細資訊，請參閱[路徑屬性](../path-properties.md)。  
  
## <a name="related-tasks"></a>相關工作  
  
-   [在資料流程路徑編輯器中檢視路徑中繼資料](../view-path-metadata-in-the-data-flow-path-editor.md)  
  
-   [連接資料流程中的元件](connect-components-in-a-data-flow.md)  
  
## <a name="see-also"></a>另請參閱  
 [資料流程](data-flow.md)  
  
  
