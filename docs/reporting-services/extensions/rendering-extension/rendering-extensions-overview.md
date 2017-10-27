---
title: "轉譯延伸模組概觀 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- formats [Reporting Services], rendering extensions
- rendering extensions [Reporting Services], about extensions
ms.assetid: 909356a0-4709-43e5-b597-33bd9bb22882
caps.latest.revision: 41
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: bf4ef7421e85e95d40a28803adec2c279b9a80bc
ms.contentlocale: zh-tw
ms.lasthandoff: 08/12/2017

---
# <a name="rendering-extensions-overview"></a>轉譯延伸模組概觀
  轉譯延伸模組是報表伺服器的元件或模組，可將報表資料與配置資訊轉換成裝置特定的格式。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]包含七個轉譯延伸模組： HTML、 Excel、 Word、 CSV 或文字、 XML、 影像和 PDF。 您可以建立其他轉譯延伸模組，以產生其他格式的報表。  
  
> [!NOTE]  
>  若要決定可以使用哪些轉譯延伸模組，您可以檢視在 RSReportServer.config 檔案中已安裝的延伸模組清單。  
  
 下表說明 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 隨附的轉譯延伸模組。  
  
|Extension Name|Description|  
|--------------------|-----------------|  
|**XML**|以 XML 格式轉譯報表。 報表會在瀏覽器中開啟。 套用至此 XML 輸出的其他轉譯，有可能是避免開發自己的轉譯延伸模組之具成本效益的方式。|  
|**CSV**|以逗號分隔格式來轉譯報表。 在與 CSV 檔案格式相關聯的檢視工具中開啟此報表。|  
|**IMAGE**|以頁面導向格式轉譯報表。 此格式在報表工具列的 [匯出] 下拉式清單中會顯示為 [TIFF]。|  
|**PDF**|在 Adobe Acrobat Reader 中轉譯報表。 此格式在報表工具列的 [匯出] 下拉式清單中會顯示為 [Acrobat (PDF) 檔案]。|  
|**EXCEL**|在 [!INCLUDE[ofprexcel](../../../includes/ofprexcel-md.md)] 中轉譯報表。|  
|**WORD**|在 [!INCLUDE[ofprword](../../../includes/ofprword-md.md)] 中轉譯報表。|  
|**HTML 4.0** （HTML 轉譯延伸模組的一部分）|HTML 是用以初始化轉譯報表的格式。 如果瀏覽器支援 HTML 4.0，就會使用此格式。 否則，系統會使用 HTML 3.2。|  
|**MHTML** （HTML 轉譯延伸模組的一部分）|以 MHTML 格式轉譯報表。 報表就會在 Internet Explorer 中開啟。 此格式在報表工具列的 [匯出] 下拉式清單中會顯示為 [網頁封存]。|  
|**NULL**|不會將報表轉譯為特定格式。 這個轉譯延伸模組對於將報表放在快取中特別有用。 Null 轉譯應該與排程執行或傳遞一起使用。|  
  
 如需有關建議的格式以及它們的用法的詳細資訊，請參閱[匯出報表 &#40;報表產生器及 SSRS &#41;](../../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md).  
  
 由 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 實作且隨附在 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中的每個轉譯模組會使用一組共同的介面。 這可確保每個延伸模組會實作相當的功能，並降低報表伺服器核心中之轉譯程式碼的複雜度。  
  
## <a name="rendering-object-model"></a>轉譯物件模型  
 當處理報表時，結果是公開的物件模型，又稱為轉譯物件模型 (ROM)。 轉譯物件模型是類別的集合，定義了已經處理的報表之內容、配置和資料。 ROM 可供開發人員設計、開發和部署 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 的自訂轉譯延伸模組。 當報表伺服器處理報表的 XML 定義以及使用者定義的報表資料時，會產生 ROM。 當處理完成時，轉譯延伸模組會使用公用物件模組，來定義報表的輸出。 ROM 的可用公用類別定義於**Microsoft.ReportingServices.OnDemandReportRendering**命名空間。  
  
## <a name="writing-custom-rendering-extensions"></a>撰寫自訂轉譯延伸模組  
 在您決定建立自訂轉譯延伸模組之前，應該先評估更簡單的替代方案。 您可以：  
  
-   透過為現有的轉譯延伸模組指定裝置資訊設定，以自訂轉譯的輸出。  
  
-   透過將 XSL 轉換 (XSLT) 與 XML 轉譯格式的輸出結合，加入自訂格式與簡報功能。  
  
 撰寫自訂轉譯延伸模組是很困難的。 轉譯延伸模組通常必須支援所有可能的報表元素結合，並需要您實作數百個類別、介面和屬性。 如果您必須轉譯報表中不含格式[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]並決定撰寫您自己的 managed 程式碼實作轉譯延伸模組的轉譯延伸模組程式碼必須實作**Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension**由報表伺服器所需的介面。  
  
 如需 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 的補充文件與白皮書，請參閱 [Reporting Services 網站](http://go.microsoft.com/fwlink/?LinkId=19951)的最新技術資源。  
  
## <a name="see-also"></a>另請參閱  
 [實作轉譯延伸模組](../../../reporting-services/extensions/rendering-extension/implementing-a-rendering-extension.md)   
 [Reporting Services 延伸模組程式庫](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  

