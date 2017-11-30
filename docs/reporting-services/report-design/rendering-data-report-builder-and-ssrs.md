---
title: "轉譯資料 (報表產生器及 SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a458fdf9-fb2a-4fee-9fbd-b38f36e91753
caps.latest.revision: "6"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: f3f2e9c9028e434482e8eadeb8f8e06ccce82987
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="rendering-data-report-builder-and-ssrs"></a>轉譯資料 (報表產生器及 SSRS)
  使用配置轉譯器 (例如 HTML、MHTML、Word、Excel、PDF 或影像) 時，資料及其組織會保持不變。 使用資料轉譯器格式 (例如，逗號分隔值 (CSV) 或 XML) 匯出時，不會轉譯任何視覺化配置元素。 轉譯報表時，CSV 和 XML 會將某些規則套用到報表主體及其內容。 這些規則決定了如何以這些格式轉譯資料。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 您可以使用資料轉譯器：  
  
-   匯入到資料庫。 CSV 是種常見的格式，能夠利用多種資料庫應用程式輕鬆匯入，包括 SQL Server 和 Microsoft Access。  
  
-   匯入到 Excel。 使用 CSV 轉譯器，將您的資料匯出到沒有視覺化配置的 Excel。 在您的資料匯到 Excel 後，您就可以使用 Excel 的標準工具，例如，圖表、公式以及樞紐資料表。  
  
-   XSLT 轉換。 XSLT 可以套用到 XML 轉譯器的輸出。 這個伺服器端的轉換是一種非常強大的技術，可以將您的資料實際上轉換為任何格式。  
  
-   資料交換/EDI。 這是一種外部程序，可以要求報表進行 CSV 或 XML 轉譯，並取用該資料。  
  
 資料轉譯器格式是由一組不同於配置轉譯器的屬性來控制。 下列是在 [屬性] 窗格中設定的屬性清單，這些屬性僅適用於資料轉譯器：  
  
-   DataElementOutput 屬性控制匯出時是否要在資料中顯示特定的項目。  
  
-   DataElementName 屬性控制資料元素的名稱。 在 CSV 中，這個屬性控制 CSV 資料行標頭的名稱。 在 XML 中，這個屬性則會變成 XML 元素的名稱或項目的屬性。  
  
-   DataElementStyle 屬性控制報表項目在 XML 中是否要轉譯為元素或屬性。  
  
 CSV 匯出選項會將報表資料儲存為逗號分隔的純文字檔案，沒有任何格式。 根據預設，此檔案使用逗號 (,) 來分隔欄位與資料列，但是此設定可以使用 [裝置資訊設定] 設定。 產生的檔案可以使用試算表程式 (例如 Office SharePoint Server) 開啟，或用來當做其他程式的匯入格式。 .csv 檔案可以使用文字編輯器 (例如 [記事本]) 開啟。 如果以 URL 存取，則 .csv 檔案會傳回 **text/csv**類型的 MIME。 檔案的 MIME 版本為 1.0。 如需以 CSV 檔案類型轉譯報表的詳細資訊，請參閱[匯出至 CSV 檔案 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-builder/exporting-to-a-csv-file-report-builder-and-ssrs.md)。  
  
 具有報表資料的 XML 檔案匯出選項會將報表儲存為 XML 檔案。 報表的 XML 結構描述為報表特有的。 XML 匯出選項不會儲存報表配置資訊。 使用此選項產生的 XML 可以匯入資料庫 (當做 XML 資料訊息)，或傳送到自訂應用程式。 如需以 XML 檔案類型轉譯報表的詳細資訊，請參閱[匯出至 XML &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-builder/exporting-to-xml-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 中的分頁 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [轉譯行為 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [不同報表轉譯延伸模組的互動式功能 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [轉譯報表項目 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [資料表、矩陣和清單 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Reporting Services 裝置資訊設定](http://go.microsoft.com/fwlink/?LinkId=102515)  
  
  
