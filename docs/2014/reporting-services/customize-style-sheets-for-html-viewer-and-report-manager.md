---
title: 自訂 HTML 檢視器和報表管理員的樣式表單 |Microsoft Docs
ms.prod: sql-server-2014
ms.technology: reporting-services-native
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 04/26/2019
ms.openlocfilehash: 7c7745d69e234f81c2a331d214789e93e9fd4014
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "64568261"
---
# <a name="customize-style-sheets-for-html-viewer-and-report-manager"></a>自訂 HTML 檢視器及報表管理員的樣式表
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]提供預設的級聯樣式表（.css）檔案，這些檔案會定義 HTML 檢視器中**報表**工具列的樣式，以及報表管理員。 如果您是 Web 開發者，或您有建立階層式樣式表的專業知識，您可以修改預設樣式 (自行負責風險)，來變更工具列或報表管理員的色彩、字型和配置。 此版本未收錄預設樣式表或樣式表的修改指示。  
  
 以不正確的方式修改樣式表，可能會導致在開啟報表時發生錯誤。 如果您不知道如何修改樣式表，請使用預設的樣式表。 如果您選擇自訂樣式表，請務必在進行任何修改之前建立所有預設 .css 檔的備份。  
  
 修改樣式表對執行於報表伺服器上的已發行報表之外觀沒有影響。 在 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]中，報表不會參考樣式表。 報表伺服器自動產生的特定報表，會使用儲存在報表伺服器程式檔案中做為內嵌資源的樣式資訊。 您在報表設計師中建立的報表，會使用您在報表定義中指定的字型、色彩和配置。 樣式會搭配配置的剩餘部分內嵌建立。  
  
> [!NOTE]  
>  如果您要使用預先定義的報表樣式，請利用「報表精靈」來建立報表。 「報表精靈」提供各種主旨，可讓您用來建立使用不同色彩組合和字型的樣式化報表。 您可以修改定義報表主旨的樣式範本。  
  
## <a name="reporting-services-style-sheets"></a>Reporting Services 樣式表  
 下表描述用於 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 安裝的樣式表 (.css) 檔案。  
  
|樣式表|描述|  
|-----------------|-----------------|  
|Htmlviewer.css|提供範例樣式表做為範本，讓您用來建立 HTML 檢視器中 **[報表]** 工具列的自訂樣式。<br /><br /> HTML 檢視器所使用的預設樣式會編譯至報表伺服器中。 Htmlviewer.css 檔提供檢視器使用的樣式範例。|  
|ReportingServices.css|定義報表管理員的樣式。|  
  
## <a name="configuring-reporting-services-to-use-a-custom-style-sheet"></a>設定 Reporting Services 來使用自訂樣式表  
 樣式表必須是有效的階層式樣式表 (.css) 檔案，且必須位於 [Styles] 資料夾中。 根據預設，[樣式] 資料夾位於\< *drive*>： \Program Files\Microsoft SQL Server\MSSQL。*n*\Reporting services\reportserver\styles。  
  
 若要在執行階段使用 HTML 檢視器的自訂樣式表，您可以從下列方式選擇：  
  
-   將 <`HTMLViewerStyleSheet`> 設定新增至[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]設定檔。  
  
-   在報表 URL 上指定樣式表。  
  
### <a name="modifying-the-rsreportserverconfig-file"></a>修改 RSReportServer.config 檔  
 您可以修改 RSReportServer.config 檔來指定 HTML 檢視器的自訂樣式表。 預設不`HTMLViewerStyleSheet`會在檔案中包含 <> 設定。 您必須在 Rsreportserver.config 的 [<`Configuration`> 選取專案中輸入該檔案，然後指定您要使用的樣式表單。 指定樣式表時，請不要包含 .css 檔延伸模組。  
  
 下列範例說明如何指定樣式表：  
  
```  
<Configuration>  
...  
          <HTMLViewerStyleSheet>MyStyleSheet</HTMLViewerStyleSheet>  
...  
</Configuration>  
```  
  
### <a name="specifying-a-style-sheet-on-a-report-url"></a>在報表 URL 上指定樣式表  
 您可以使用 `rc:StyleSheet` URL 存取參數，在報表 URL 上指定自訂樣式表。 如需如何指定 URL 存取參數的詳細資訊，請參閱[Url 存取參數參考](url-access-parameter-reference.md)。  
  
 下列範例說明如何加入自訂樣式：  
  
```  
http://localhost/reportserver?/AdventureWorksSampleReports/Product+Line+Sales&rs:Command=Render&rc:Stylesheet=MyStyleSheet  
```  
  
## <a name="see-also"></a>另請參閱  
 [報表管理員 &#40;SSRS 原生模式&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [HTML 檢視器和報告工具列](html-viewer-and-the-report-toolbar.md)   
 [RSReportServer Configuration File](report-server/rsreportserver-config-configuration-file.md)  
  
  
