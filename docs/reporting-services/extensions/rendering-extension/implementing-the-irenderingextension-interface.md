---
title: 實作 IRenderingExtension 介面 | Microsoft Docs
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.suite: pro-bi
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- IRenderingExtension interface
- rendering extensions [Reporting Services], IRenderingExtension interface
ms.assetid: 74b2f2b7-6796-42da-ab7d-b05891ad4001
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5526129418f454f7323add732458081f5db11869
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2018
ms.locfileid: "43274460"
---
# <a name="implementing-the-irenderingextension-interface"></a>實作 IRenderingExtension 介面
  轉譯延伸模組會從與實際資料結合的報表定義取得結果，並將產生的資料轉譯成可用的格式。 結合的資料與格式之轉換是利用實作 <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension> 的 Common Language Runtime (CLR) 類別來完成。 這可將物件模型轉換為檢視器、印表機或是其他輸出目標可取用的輸出格式。  
  
 <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension> 具有三個必須撰寫程式碼的方法：  
  
-   <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.Render%2A> - 轉譯報表。  
  
-   <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.RenderStream%2A> - 從報表轉譯特定的資料流。  
  
-   <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.GetRenderingResource%2A> - 取得報表所需的其他資訊，例如圖示。  
  
 下列各節針對這些方法進行更詳細的討論。  
  
## <a name="render-method"></a>Render 方法  
 <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.Render%2A> 方法包含代表下列物件的引數：  
  
-   您要轉譯的「報表」。 這個物件包含報表的屬性、資料與配置資訊。 報表是報表物件模型樹狀結構的根目錄。  
  
-   包含字串字典物件的 *ServerParameters*，含報表伺服器的參數 (如果有的話)。  
  
-   包含裝置設定的 *deviceInfo* 參數。 如需詳細資訊，請參閱[將裝置資訊設定傳遞至轉譯延伸模組](../../../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)。  
  
-   包含 <xref:System.Collections.Specialized.NameValueCollection> 字典物件的 *clientCapabilities* 參數，該物件具有您要轉譯之目標用戶端的資訊。  
  
-   包含轉譯結果相關資訊的 *RenderProperties*。  
  
-   *createAndRegisterStream* 是要呼叫的委派函式，以取得要轉譯成的資料流。  
  
### <a name="deviceinfo-parameter"></a>deviceInfo 參數  
 *deviceInfo* 參數包含轉譯參數，而不是報表參數。 這些轉譯參數會傳遞給轉譯延伸模組。 報表伺服器會將 *deviceInfo* 值轉換為 <xref:System.Collections.Specialized.NameValueCollection> 物件。 在 *deviceInfo* 參數中的項目會視為不區分大小寫的值。 如果轉譯要求是以 URL 存取的結果呈現，則 `rc:key=value` 格式的 URL 參數會轉換成 *deviceInfo* 字典物件中的索引鍵/值組。 瀏覽器偵測程式碼也在 *clientCapabilities* 字典中提供下列項目：EcmaScriptVersion、JavaScript、MajorVersion、MinorVersion、Win32、Type 及 AcceptLanguage。 會忽略在 *deviceInfo* 參數中轉譯延伸模組不了解的任何名稱/值組。 下列程式碼範例顯示用來擷取圖示的範例 <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.GetRenderingResource%2A> 方法：  
  
```csharp  
public void GetRenderingResource (CreateStream createStreamCallback, NameValueCollection deviceInfo)  
{  
    string[] iconTagValues = deviceInfo.GetValues("Icon");  
    if ((iconTagValues != null) && (iconTagValues.Length > 0) )  
    {  
        // Create a stream to output to.  
        Stream outputStream = createStreamCallback(m_iconResourceName, "gif", null, "image/gif", false);  
        // Get the GIF image for one of the buttons on the toolbar  
        Image requiredImage = (Image) m_resourcemanager.GetObject(m_iconResourceName  
        // Write the image to the output stream  
        requiredImage.Save(outputStream, requiredImage.RawFormat);  
    }  
    return;  
}  
```  
  
## <a name="renderstream-method"></a>RenderStream 方法  
 <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.RenderStream%2A> 方法會從報表轉譯特定的資料流。 在初始 <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.Render%2A> 呼叫期間會建立所有的資料流，但是一開始不會將資料流傳回給用戶端。 這個方法是用於第二個資料流 (例如 HTML 轉譯中的影像) 或是多頁面轉譯延伸模組的其他頁面 (例如影像/EMF)。  
  
## <a name="getrenderingresource-method"></a>GetRenderingResource 方法  
 <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.GetRenderingResource%2A> 方法會擷取資訊，而不需執行報表的完整轉譯。 有時報表需要的資訊，並不需要轉譯報表本身。 例如，如果您需要與轉譯延伸模組建立關聯的圖示，請使用包含單一標記 **\<Icon>** 的 *deviceInfo* 參數。 在這些情況下，您可以使用 <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.GetRenderingResource%2A> 方法。  
  
## <a name="see-also"></a>另請參閱  
 [實作轉譯延伸模組](../../../reporting-services/extensions/rendering-extension/implementing-a-rendering-extension.md)   
 [轉譯延伸模組概觀](../../../reporting-services/extensions/rendering-extension/rendering-extensions-overview.md)  
  
  
