---
title: ODBC 來源 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.odbcsource.f1
ms.assetid: abcf34eb-9140-4100-82e6-b85bccd22abe
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d125a725a9e1c0cab34c7066fd9554ef0099d6e6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62901103"
---
# <a name="odbc-source"></a>ODBC 來源
  ODBC 來源會使用資料庫資料表、檢視或 SQL 陳述式，從 ODBC 支援的資料庫中擷取資料。  
  
 ODBC 來源有下列資料存取模式可供擷取資料：  
  
-   資料表或檢視。  
  
-   SQL 陳述式的結果。  
  
 來源使用 ODBC 連接管理員，指定要使用的提供者。  
  
 ODBC 來源包含來源資料輸出資料行。 在 ODBC 目的地中將輸入資料行對應到目的地資料行時，如果沒有輸入資料行對應到目的地資料行，可能會發生錯誤。 可對應不同類型的資料行，但是如果輸出資料與目的地不相容，在執行階段會發生錯誤。 根據錯誤行為設定，錯誤會被忽略，導致失敗，或者資料列會傳送至錯誤輸出。  
  
 ODBC 來源有一個一般輸出和一個錯誤輸出。  
  
## <a name="error-handling"></a>錯誤處理  
 ODBC 來源有錯誤輸出。 此元件的錯誤輸出包含下列輸出資料行：  
  
-   **錯誤碼**：對應至目前錯誤的編號。 請參閱 ODBC 支援的資料庫的文件集，以取得錯誤清單。 如需 SSIS 錯誤碼清單，請參閱＜SSIS 錯誤碼和訊息參考＞。  
  
-   **錯誤資料行**：造成錯誤 (用於轉換錯誤) 的來源資料行。  
  
-   標準輸出資料行。  
  
 根據錯誤行為設定，ODBC 來源支援在錯誤輸出中傳回擷取程序期間發生的錯誤 (資料轉換、截斷)。 如需詳細資訊，請參閱 [ODBC 目的地編輯器 &#40;連線管理員頁面&#41;](../odbc-destination-editor-connection-manager-page.md)。  
  
## <a name="data-type-support"></a>資料類型支援  
 如需有關 ODBC 來源支援之資料類型的資訊，請參閱＜Connector for Open Database Connectivity (ODBC) by Attunity＞。  
  
## <a name="extract-options"></a>擷取選項  
 ODBC 來源以 [批次] 或 [逐列] 模式操作。 所用的模式是由 **FetchMethod** 屬性所決定。 下列清單描述這些模式。  
  
-   **批次**：元件會根據所見的 ODBC 提供者功能，嘗試使用最有效率的擷取方法。 對於最新型的 ODBC 提供者，這是 SQLFetchScroll 與陣列繫結搭配使用 (陣列大小是由 **BatchSize** 屬性所決定)。 如果您選取 [批次]，而提供者不支援此方法，ODBC 目的地會自動切換為**逐列**模式。  
  
-   **逐列**：元件會使用 SQLFetch，一次擷取一個資料列。  
  
 如需有關 **FetchMethod** 屬性的詳細資訊，請參閱＜ [ODBC Source Custom Properties](odbc-source-custom-properties.md)＞。  
  
## <a name="parallelism"></a>平行處理原則  
 可針對相同電腦或不同電腦上的相同資料表或不同資料表平行執行的 ODBC 來源元件數目不受限制 (除了一般全域工作階段限制之外)。  
  
 然而，所使用的 ODBC 提供者的限制可能會限制透過提供者的並行連接數目。 這些限制會限制 ODBC 來源支援的平行執行個體數目。 SSIS 開發人員必須知道所使用的任何 ODBC 提供者的限制，並在建立 SSIS 封裝時將這些限制納入考量。  
  
## <a name="troubleshooting-the-odbc-source"></a>ODBC 來源的疑難排解  
 您可以記錄 ODBC 來源對外部資料提供者所執行的呼叫。 您可以使用這項記錄功能，疑難排解 ODBC 來源執行的從外部資料來源載入資料的作業。 若要記錄 ODBC 來源對外部資料提供者執行的呼叫，請啟用 ODBC 驅動程式管理員追蹤。 如需詳細資訊，請參閱 Microsoft 文件集＜如何使用 ODBC 資料來源管理員產生 ODBC 追蹤＞。   
  
## <a name="configuring-the-odbc-source"></a>設定 ODBC 來源  
 您可以透過程式設計方式或 SSIS 設計師來設定 ODBC 來源。  
  
 如需詳細資訊，請參閱下列其中一個主題：  
  
-   [ODBC 來源編輯器 &#40;連線管理員頁面&#41;](../odbc-source-editor-connection-manager-page.md)  
  
-   [ODBC 來源編輯器 &#40;資料行頁面&#41;](../odbc-source-editor-columns-page.md)  
  
-   [ODBC 來源編輯器 &#40;錯誤輸出頁面&#41;](../odbc-source-editor-error-output-page.md)  
  
 **[進階編輯器]** 對話方塊包含可以程式設計方式設定的屬性。  
  
 若要開啟 **[進階編輯器]** 對話方塊：  
  
-   在 **專案的** [資料流程] [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 畫面中，以滑鼠右鍵按一下 ODBC 來源，然後選取 **[顯示進階編輯器]**。  
  
 如需有關可在 [進階編輯器] 對話方塊中設定之屬性的詳細資訊，請參閱＜ [ODBC Source Custom Properties](odbc-source-custom-properties.md)＞。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [ODBC 來源編輯器 &#40;錯誤輸出頁面&#41;](../odbc-source-editor-error-output-page.md)  
  
-   [ODBC 來源編輯器 &#40;資料行頁面&#41;](../odbc-source-editor-columns-page.md)  
  
-   [ODBC 來源編輯器 &#40;連線管理員頁面&#41;](../odbc-source-editor-connection-manager-page.md)  
  
-   [使用 ODBC 來源來擷取資料](odbc-source.md)  
  
-   [ODBC Source Custom Properties](odbc-source-custom-properties.md)  
  
  
