---
title: "ODBC 目的地 |Microsoft 文件"
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
- sql13.ssis.designer.odbcdest.f1
ms.assetid: bffa63e0-c737-4b54-b4ea-495a400ffcf8
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5947fa19295580396ce74f8dd93f75abed653797
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="odbc-destination"></a>ODBC 目的地
  ODBC 目的地會將資料大量載入到 ODBC 支援的資料庫資料表。 ODBC 目的地使用 ODBC 連接管理員來連接到資料來源。  
  
 ODBC 目的地包含輸入資料行與目的地資料來源中資料行之間的對應。 您不一定要將輸入資料行對應到所有目的地資料行，但因目的地資料行屬性的不同，如果輸入資料行未對應到目的地資料行，則可能發生錯誤。 例如，如果目的地資料行不允許 Null 值，則輸入資料行必須對應到該資料行。 此外，雖然可對應不同類型的資料行，但是如果輸入資料與目的地資料行類型不相容，在執行階段會發生錯誤。 根據錯誤行為設定，錯誤會被忽略，導致失敗，或者資料列會傳送至錯誤輸出。  
  
 ODBC 目的地具有一個一般輸出和一個錯誤輸出。  
  
##  <a name="BKMK_odbcdestination_loadoptions"></a> 載入選項  
 ODBC 目的地可以使用兩種存取載入模組其中之一。 您會在 [ODBC 來源編輯器 &#40;連線管理員頁面&#41;](../../integration-services/data-flow/odbc-source-editor-connection-manager-page.md) 設定模式。 兩種模式為：  
  
-   **批次**：在此模式中，ODBC 目的地會根據所見的 ODBC 提供者功能，嘗試使用最有效率的插入方法。 對於最新的 ODBC 提供者，這表示準備含有參數的 INSERT 陳述式，然後使用資料列取向的陣列參數繫結 (陣列大小是由 **BatchSize** 屬性所控制)。 如果您選取 [批次]，而提供者不支援此方法，ODBC 目的地會自動切換為**逐列**模式。  
  
-   **逐列**：在此模式中，ODBC 目的地會準備含有參數的 INSERT 陳述式，然後使用 **SQL Execute**，一次插入一個資料列。  
  
## <a name="error-handling"></a>錯誤處理  
 ODBC 目的地有錯誤輸出。 此元件的錯誤輸出包含下列輸出資料行：  
  
-   **錯誤碼**：對應至目前錯誤的編號。 如需錯誤清單，請參閱來源資料庫的文件集。 如需 SSIS 錯誤碼清單，請參閱＜SSIS 錯誤碼和訊息參考＞。  
  
-   **錯誤資料行**：造成錯誤 (用於轉換錯誤) 的來源資料行。  
  
-   標準輸出資料行。  
  
 根據錯誤行為設定，ODBC 目的地支援在錯誤輸出中傳回擷取程序期間發生的錯誤 (資料轉換、截斷)。 如需詳細資訊，請參閱 [ODBC 來源編輯器 &#40;錯誤輸出頁面&#41;](../../integration-services/data-flow/odbc-source-editor-error-output-page.md)。  
  
## <a name="parallelism"></a>平行處理原則  
 可針對相同電腦或不同電腦上的相同資料表或不同資料表平行執行的 ODBC 目的地元件數目不受限制 (除了一般全域工作階段限制之外)。  
  
 然而，所使用的 ODBC 提供者的限制可能會限制透過提供者的並行連接數目。 這些限制會限制 ODBC 目的地支援的平行執行個體數目。 SSIS 開發人員必須知道所使用的任何 ODBC 提供者的限制，並在建立 SSIS 封裝時將這些限制納入考量。  
  
 您還必須知道同時載入到相同資料表可能會因為標準記錄鎖定而降低效能。 這取決於正在載入的資料和資料表組織。  
  
## <a name="troubleshooting-the-odbc-destination"></a>ODBC 目的地疑難排解  
 您可以記錄 ODBC 來源對外部資料提供者所執行的呼叫。 您可以使用這項記錄功能，針對 ODBC 目的地所執行之將資料儲存至外部資料來源的作業進行疑難排解。 若要記錄 ODBC 目的地對外部資料提供者執行的呼叫，請啟用 ODBC 驅動程式管理員追蹤。 如需詳細資訊，請參閱 Microsoft 文件集＜如何使用 ODBC 資料來源管理員產生 ODBC 追蹤＞。   
  
## <a name="configuring-the-odbc-destination"></a>設定 ODBC 目的地  
 您可以透過程式設計方式或 SSIS 設計師來設定 ODBC 目的地。  
  
 如需詳細資訊，請參閱下列其中一個主題：  
  
-   [ODBC 目的地編輯器 &#40;連接管理員頁面 &#41;](../../integration-services/data-flow/odbc-destination-editor-connection-manager-page.md)  
  
-   [ODBC 目的地編輯器 &#40;[對應] 頁面 &#41;](../../integration-services/data-flow/odbc-destination-editor-mappings-page.md)  
  
-   [ODBC 目的地編輯器 &#40;錯誤輸出頁面 &#41;](../../integration-services/data-flow/odbc-destination-editor-error-output-page.md)  
  
 **[進階編輯器]** 對話方塊包含可以程式設計方式設定的屬性。  
  
 若要開啟 **[進階編輯器]** 對話方塊：  
  
-   在 **專案的** [資料流程] [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 畫面中，以滑鼠右鍵按一下 ODBC 目的地，然後選取 **[顯示進階編輯器]**。  
  
 如需有關可在 [進階編輯器] 對話方塊中設定之屬性的詳細資訊，請參閱＜ [ODBC Destination Custom Properties](../../integration-services/data-flow/odbc-destination-custom-properties.md)＞。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [ODBC 目的地編輯器 &#40;錯誤輸出頁面 &#41;](../../integration-services/data-flow/odbc-destination-editor-error-output-page.md)  
  
-   [ODBC 目的地編輯器 &#40;[對應] 頁面 &#41;](../../integration-services/data-flow/odbc-destination-editor-mappings-page.md)  
  
-   [ODBC 目的地編輯器 &#40;連接管理員頁面 &#41;](../../integration-services/data-flow/odbc-destination-editor-connection-manager-page.md)  
  
-   [使用 ODBC 目的地載入資料](../../integration-services/data-flow/load-data-by-using-the-odbc-destination.md)  
  
-   [ODBC 目的地自訂屬性](../../integration-services/data-flow/odbc-destination-custom-properties.md)  
  
  
