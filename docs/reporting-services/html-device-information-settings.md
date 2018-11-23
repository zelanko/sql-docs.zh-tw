---
title: HTML 裝置資訊設定 | Microsoft Docs
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- HTML [Reporting Services], rendering
- device information settings [Reporting Services], HTML rendering
ms.assetid: f505f478-dd6d-444a-957c-34f7cfb98911
author: markingmyname
ms.author: maghan
ms.openlocfilehash: df7cb6c2f5c04138d6738eadeb9b352d21f240f5
ms.sourcegitcommit: 9ece10c2970a4f0812647149d3de2c6b75713e14
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/16/2018
ms.locfileid: "51813681"
---
# <a name="html-device-information-settings"></a>HTML 裝置資訊設定
下表列出以 HTML 格式轉譯的裝置資訊設定。  
  
> [!IMPORTANT]  
>  下表所列出帶有 **(\*)** 的裝置資訊設定已被取代，不應在新的應用程式中使用。 如需詳細資訊，請參閱 [SQL Server 2016 中 SQL Server Reporting Services 已被取代的功能](../reporting-services/deprecated-features-in-sql-server-reporting-services-ssrs.md)   
  
|設定|ReplTest1|  
|-------------|-----------|  
|**AccessibleTablix**|指出是否要使用其他可存取性中繼資料來轉譯，以搭配螢幕助讀員使用。 其他可存取性中繼資料會使得轉譯的報表與下列文件內的技術標準相容：＜Electronic and Information Technology Accessibility Standards＞文件 (章節 508) 的＜Web-based Intranet and Internet Information and Applications＞章節 (1194.22)。<br /><br /> (g) 應該針對資料表識別資料列和資料行標頭。<br /><br /> (h) 如果資料表具有兩個或多個邏輯層的資料列或資料行標頭，應該使用標記來讓資料格與標頭資料格產生關聯。|  
|**ActionScript(\*)**|指定發生動作事件 (例如鑽研或書籤點擊) 時所要使用之 JavaScript 函數的名稱。 如果指定這個參數，動作事件便會觸發具名 JavaScript 函數，而非回傳至伺服器。|  
|**BookmarkID**|跳到報表中的書籤識別碼。|  
|**DocMap**|指出是否要顯示或隱藏報表文件引導模式。 此參數的預設值為 **true**。|  
|**ExpandContent**|指出報表是否應該包括在限制水平大小的表格結構中。|  
|**FindString**|報表中要搜尋的文字。 這個參數的預設值為空字串。|  
|**GetImage (\*)**|取得 HTML 檢視器使用者介面的特定圖示。|  
|**HTMLFragment**|指出是否建立 HTML 片段來取代完整的 HTML 文件。 HTML 片段會在 TABLE 元素中包含報表內容，並省略 HTML 和 BODY 元素。 預設值為 **false**。 如果您使用 SOAP API 的 **M:ReportExecution2005.ReportExecutionService.Render(System.String,System.String,System.String@,System.String@,System.String@, ReportExecution2005.Warning[]@,System.String[]@)** 方法來轉譯為 HTML，而且若是轉譯的報表含有影像，則需要將此裝置資訊設定為 **true** 。 轉譯時使用含有將 **HTMLFragment** 屬性設定為 **true** 的 SOAP，會建立包含工作階段的資訊，這些資訊可用以正確地要求影像。 影像必須是報表伺服器資料庫中上傳的資源。|  
|**ImageConsolidation**|指出是否要將轉譯的圖表、地圖、量測計和指標影像合併成一個大型影像。 當報表包含許多資料視覺效果項目時，影像的合併有助於改良用戶端瀏覽器中報表的效能。 對於大多數最新型的瀏覽器而言，預設值為 **true** 。|  
|**JavaScript**|指出在轉譯的報表中是否支援 JavaScript。 預設值為 **true**。|  
|**LinkTarget**|報表中超連結的目標。 透過提供視窗名稱，可將視窗或框架作為目標，像是 **LinkTarget**=*window_name*或是您可以使用 **LinkTarget**=_blank 以新視窗為目標。 其他有效的目標名稱包括 _self, _parent, and _top。|  
|**OnlyVisibleStyles(\*)**|指出只會產生目前轉譯頁面的共用樣式。|  
|**OutlookCompat**|指出是否要使用額外中繼資料轉譯，讓報表在 Outlook 中有較佳的外觀。 對於其他人，預設值為 **false**。|  
|**參數**|指出是否要顯示或隱藏工具列的參數區。 如果將這個參數設定為 **true**的值，就會顯示工具列的參數區域。 此參數的預設值為 **true**。|  
|**PrefixId**|搭配 **HTMLFragment**使用時，會在已建立的 HTML 片段中的所有 **ID** 屬性加入指定的前置詞。|  
|**ReplacementRoot(\*)**|在 ReportViewer 控制項之外轉譯時，在報表中所有鑽研、切換和書籤連結之前附加的字串。 例如，這個字串可用來將使用者的按鍵動作重新導向至自訂網頁。|  
|**ResourceStreamRoot(\*)**|所有影像資源 (例如切換或排序的影像) 的 URL 前面所要加上的字串。|  
|**章節**|要轉譯之報表的頁碼。 **0** 的值表示轉譯報表的所有區段。 預設值是 **1**秒。|  
|**StreamRoot (\*)**|這個路徑會加在報表伺服器傳回的 HTML 報表中的 IMG 元素之 **src** 屬性值前面。 依預設，報表伺服器會提供路徑。 您可以使用此設定為報表中的影像指定根路徑 (例如，**https://\<伺服器名稱>/resources/companyimages**)。|  
|**StyleStream**|指出是否將樣式和指令碼建立成不同的資料流，而不是在文件中。 預設值為 **false**。|  
|**工具列**|指出是否要顯示或隱藏工具列。 這個參數的預設值為 **true**。 如果這個參數的值為 **false**，則會忽略所有剩餘的選項 (文件引導模式除外)。 如果您省略這個參數，工具列就會自動顯示以轉譯支援該參數的格式。<br /><br /> 當您使用 URL 存取來轉譯報表時，會轉譯報表檢視器工具列。 工具列不是透過 SOAP API 來轉譯。 不過， **Toolbar** 裝置資訊設定會影響使用 SOAP **Render** 方法時顯示報表的方式。 如果此參數值在使用 SOAP 轉譯為 HTML 時為 **true** ，則會轉譯報表的第一個區段。 如果值是 **false**，則會將整個 HTML 報表轉譯為單一 HTML 頁面。|  
|**UserAgent**|提出要求之瀏覽器的 **user-agent** 字串，該字串可在 HTTP 要求中找到。|  
|**Zoom (\*)**|報表縮放值，以整數百分比或字串常數表示。 標準字串值包括 **Page Width** 和 **Whole Page**。 Internet Explorer 5.0 之前的 [!INCLUDE[msCoName](../includes/msconame-md.md)] Internet Explorer 版本和所有非[!INCLUDE[msCoName](../includes/msconame-md.md)] 瀏覽器都會忽略這個參數。 此參數的預設值為 **100**。|  
|**DataVisualizationFitSizing**|指示資料在 Tablix 內的視覺效果調整行為。 其中包括圖表、量測計和地圖。<br /><br /> 可能的值為 **[近似]** 和 **[精確]**。<br /><br /> 預設值為 **[近似]**。 如果從 **rsreportserver.config** 檔案中移除此設定，則預設行為是 **[精確]**。<br /><br /> 啟用 **[精確]** 可能會影響效能，因為判斷精確大小的處理所花的時間可能會比較長。|  
  
## <a name="see-also"></a>另請參閱  
 [將裝置資訊設定傳遞至轉譯延伸模組](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [在 RSReportServer.Config 中自訂轉譯延伸模組參數](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [技術參考 &#40;SSRS&#41;](../reporting-services/technical-reference-ssrs.md)  
  
  
