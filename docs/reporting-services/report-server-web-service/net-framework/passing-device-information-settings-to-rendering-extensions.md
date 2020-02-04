---
title: 將裝置資訊設定傳遞至轉譯延伸模組 | Microsoft Docs
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service
ms.topic: reference
helpviewer_keywords:
- device information settings [Reporting Services]
- Render method
- Report Server Web service, device information settings
- Web service [Reporting Services], device information settings
- XML Web service [Reporting Services], device information settings
- passing device information [Reporting Services]
- rendering extensions [Reporting Services], device information settings
- rendering [Reporting Services], settings
- device information settings [Reporting Services], about device information settings
- extensions [Reporting Services], device information settings
ms.assetid: fe718939-7efe-4c7f-87cb-5f5b09caeff4
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 4171fcbc01b7dfd36003bef6c4fa5d90c74600d3
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "63128883"
---
# <a name="passing-device-information-settings-to-rendering-extensions"></a>將裝置資訊設定傳遞至轉譯延伸模組
  在 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]中，裝置資訊設定會用於將轉譯參數傳遞給轉譯延伸模組。 Report Server Web 服務中的設定會當做 **DeviceInfo** XML 元素傳遞，並由報表伺服器進行處理。 因為裝置資訊設定具有預設值，所以這些值被視為轉譯程序中的選擇性引數。 不過，您可以使用裝置資訊設定來自訂轉譯，並覆寫伺服器所套用的預設值。  
  
 您可以用多種方法來指定裝置資訊設定。 您可以用程式設計的方式來使用 Render 方法。 如果要透過報表的 URL 存取報表，可以將裝置資訊指定為 URL 參數。 也可以在 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 組態檔中編輯裝置資訊設定，以指定全域的轉譯參數。 如需全域指定轉譯參數的詳細資訊，請參閱[在 RSReportServer.Config 中自訂轉譯延伸模組參數](../../../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)。  
  
## <a name="passing-device-information-using-the-render-method"></a>使用轉譯方法傳遞裝置資訊  
 若要將裝置資訊設定傳遞至轉譯延伸模組，請使用 **M:Microsoft.WSSUX.ReportingServicesWebService.RSExecutionService2005.ReportExecutionService.Render(System.String,System.String,System.String@,System.String@,System.String@,Microsoft.WSSUX.ReportingServicesWebService.RSExecutionService2005.Warning[]@,System.String[]@)** 方法。 例如，下列的 XML 字串可以傳遞至 <xref:ReportExecution2005.ReportExecutionService.Render%2A> 方法，以在轉譯為 HTML 時建立 HTML 片段。  
  
```  
<DeviceInfo>  
   <HTMLFragment>True</HTMLFragment>  
</DeviceInfo>  
```  
  
 當報表轉譯為 HTML 片段時，報表的內容會包含在 TABLE 元素內，而不會使用 HTML 或 BODY 元素。 您可以使用 HTML 片段來將報表整合到現有的 HTML 文件中。 如需 HTML 輸出之裝置資訊設定的詳細資訊，請參閱 [HTML 裝置資訊設定](../../../reporting-services/html-device-information-settings.md)。  
  
## <a name="passing-device-information-using-url-access"></a>使用 URL 存取傳遞裝置資訊  
 您也可以透過 URL 存取來傳遞裝置資訊設定。 裝置資訊設定會當做 URL 參數傳遞。 下列的 URL 存取字串可以傳遞至報表伺服器以產生轉譯的報表 (沒有 HTML 檢視器工具列)。  
  
```  
https://<Server Name>/reportserver?/SampleReports/Sales Order Detail&rs:Command=Render&rs:Format=HTML4.0&rc:Toolbar=False  
```  
  
 如需詳細資訊，請參閱[在 URL 中指定裝置資訊設定](../../../reporting-services/specify-device-information-settings-in-a-url.md)。  
  
## <a name="see-also"></a>另請參閱  
 [轉譯延伸模組的裝置資訊設定 &#40;Reporting Services&#41;](../../../reporting-services/device-information-settings-for-rendering-extensions-reporting-services.md)   
 [在 RSReportServer.Config 中自訂轉譯延伸模組參數](../../../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [使用 Web 服務和.NET Framework 建置應用程式](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)  
  
  
