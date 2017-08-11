---
title: "自訂轉譯延伸模組參數，在 RSReportServer.Config 中的 |Microsoft 文件"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- configuration options [Reporting Services]
- DeviceInfo settings
- rendering extensions [Reporting Services], overriding behaviors
- parameters [Reporting Services], report rendering
- overriding report rendering behavior
- extensions [Reporting Services], rendering
ms.assetid: 3bf7ab2b-70bb-41c8-acda-227994d15aed
caps.latest.revision: 31
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 009b40c83d662b40b3215f701a2eb490ebc4fed1
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="customize-rendering-extension-parameters-in-rsreportserverconfig"></a>在 RSReportServer.Config 中自訂轉譯延伸模組參數
  您可以在 RSReportServer 組態檔中指定轉譯延伸模組參數，以便覆寫在 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 報表伺服器上執行之報表的預設報表轉譯行為。 您可以修改轉譯延伸模組參數來達成下列目標：  
  
-   變更轉譯延伸模組名稱在報表工具列 [匯出] 清單中的顯示方式 (例如，將「網頁封存」變更為「MHTML」)，或者將該名稱翻譯為不同的語言。  
  
-   建立同一個轉譯延伸模組的多個執行個體，以支援不同的報表呈現選項 (例如，影像轉譯延伸模組的縱向及橫向模式版本)。  
  
-   變更預設轉譯延伸模組參數，以使用不同的值 (例如，影像轉譯延伸模組使用 TIFF 做為預設的輸出格式；您可以修改該參數，改為使用 EMF)。  
  
 變更轉譯延伸模組參數只會影響報表伺服器上的轉譯作業。 您無法覆寫報表設計師中報表預覽的轉譯延伸模組設定。  
  
 指定組態檔中的轉譯延伸模組參數，會對轉譯延伸模組造成全域的影響。 只要使用特定的轉譯延伸模組，組態檔中的設定就會取代預設值。 如果您要針對特定報表或轉譯作業設定轉譯延伸模組參數，就必須使用 <xref:ReportExecution2005.ReportExecutionService.Render%2A> 方法以程式設計的方式指定裝置資訊，或在報表 URL 上指定裝置資訊設定。 如需針對轉譯作業指定裝置資訊設定，以及檢視裝置資訊設定之完整清單的詳細資訊，請參閱 [將裝置資訊設定傳遞至轉譯延伸模組](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)。  
  
## <a name="finding-and-modifying-rsreportserverconfig"></a>尋找及修改 RSReportServer.config  
 報表輸出格式的組態設定會在 RSReportServer.config 檔中指定為轉譯延伸模組參數。 若要指定組態檔中的轉譯延伸模組參數，您必須了解如何定義設定轉譯參數的 XML 結構。 可進行修改的 XML 結構有兩種：  
  
-   **OverrideNames** 元素會定義轉譯延伸模組顯示的名稱和語言。  
  
-   **DeviceInfo** XML 結構會定義轉譯延伸模組所使用的裝置資訊設定。 大部分的轉譯延伸模組參數會指定為裝置資訊設定。  
  
 您可以使用文字編輯器來修改 RSReportServer.config 檔案， 此檔案可以在 \Reporting Services\Report Server\Bin 資料夾中找到。 如需有關修改組態檔的詳細資訊，請參閱[修改 Reporting Services 組態檔 &#40;RSreportserver.config &#41;](../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md).  
  
## <a name="changing-the-display-name"></a>變更顯示名稱  
 轉譯延伸模組的顯示名稱會出現在報表工具列的 [匯出] 清單中。 預設顯示名稱的範例包括網頁封存、TIFF 檔案和 Acrobat (PDF) 檔案。 藉著指定組態檔中的 **OverrideNames** 元素，您可以使用自訂的值來取代預設的顯示名稱。 此外，如果您正在定義單一轉譯延伸模組的兩個執行個體，也可以使用 **OverrideNames** 元素在 [匯出] 清單中區分每一個執行個體。  
  
 由於顯示名稱已經當地語系化，如果您要使用自訂的值取代預設顯示名稱，就必須設定 **Language** 屬性。 否則，任何指定的名稱都會被忽略。 您所設定的語言值，對於報表伺服器電腦必須是有效值。 例如，如果報表伺服器是在法文作業系統上執行，您應該指定「fr-FR」做為屬性值。  
  
 下列範例會說明在英文報表伺服器上提供自訂名稱的方法：  
  
```  
<Extension Name="XML" Type="Microsoft.ReportingServices.Rendering.DataRenderer.XmlDataReport,Microsoft.ReportingServices.DataRendering">  
   <OverrideNames>  
     <Name Language="en-US">My Custom Display Name for XML Rendering</Name>  
   </OverrideNames>  
</Extension>  
```  
  
## <a name="changing-device-information-settings"></a>變更裝置資訊設定  
 若要修改已經部署在您報表伺服器上之轉譯延伸模組所使用的預設裝置資訊設定，您必須在組態檔中輸入 **DeviceInfo** XML 結構。 每一個轉譯延伸模組都支援該延伸模組獨特的裝置資訊設定。 若要檢視裝置資訊設定的完整清單，請參閱 [將裝置資訊設定傳遞至轉譯延伸模組](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)。  
  
 下列範例會提供 XML 結構的說明，以及修改影像轉譯延伸模組預設設定的語法：  
  
```  
<Render>  
    <Extension Name="IMAGE (EMF)" Type="Microsoft.ReportingServices.Rendering.ImageRenderer.ImageRenderer,Microsoft.ReportingServices.ImageRendering">  
        <OverrideNames>  
            <Name Language="en-US">Image (EMF)</Name>  
        </OverrideNames>  
        <Configuration>  
            <DeviceInfo>  
                <ColorDepth>32</ColorDepth>  
                <DpiX>300</DpiX>  
                <DpiY>300</DpiY>  
                <OutputFormat>EMF</OutputFormat>  
            </DeviceInfo>  
        </Configuration>  
    </Extension>  
</Render>  
```  
  
## <a name="configuring-multiple-entries-for-a-rendering-extension"></a>設定轉譯延伸模組的多個項目  
 您可以建立同一個轉譯延伸模組的多個執行個體，以支援不同的報表呈現選項。 您定義的每個執行個體可以具有不同的參數值組合。 定義現有轉譯延伸模組的執行個體時，請務必執行下列動作：  
  
-   指定延伸模組的唯一名稱。  
  
     每個延伸模組必須具有 **Name** 屬性的唯一值。 下列範例會使用 "IMAGE (EMF Landscape)" 和 "IMAGE (EMF Portrait)" 的名稱來區分兩個執行個體。  
  
     變更已經部署之轉譯延伸模組的名稱時，要特別小心， 因為透過程式設計的方式指定轉譯延伸模組的開發人員，會使用延伸模組名稱來識別特定轉譯作業所使用的執行個體。 如果您在報表伺服器上執行自訂的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 應用程式，請確定開發人員知道您修改了現有的延伸模組名稱，或是新增了新的延伸模組名稱。  
  
-   請指定唯一的顯示名稱，如此使用者可以了解每一個輸出格式的差異。  
  
     如果您為同一個延伸模組設定多個版本，則可以提供 **OverrideNames**的值，藉此為每個版本指定一個唯一名稱。 否則，在報表工具列的 [匯出] 清單中，每個版本的延伸模組都會有相同的名稱。  
  
 下列範例說明使用預設影像轉譯延伸模組 (這會產生 TIFF 輸出) 輸出縱向模式 EMF，連同以第二個執行個體輸出橫向模式 EMF 格式報表的方法。 請注意，每個延伸模組名稱都是唯一的。 測試此範例時，請記得選擇沒有包含互動式功能 (例如顯示/隱藏選項、矩陣或鑽研連結) 的報表，因為互動式功能不能在影像轉譯延伸模組中執行：  
  
```  
<Render>  
    <Extension Name="IMAGE (EMF Landscape)" Type="Microsoft.ReportingServices.Rendering.ImageRenderer.ImageRenderer,Microsoft.ReportingServices.ImageRendering">  
        <OverrideNames>  
            <Name Language="en-US">EMF in Landscape Mode</Name>  
        </OverrideNames>  
        <Configuration>  
            <DeviceInfo>  
                <OutputFormat>EMF</OutputFormat>  
                <PageHeight>8.5in</PageHeight>  
                <PageWidth>11in</PageWidth>  
            </DeviceInfo>  
        </Configuration>  
    </Extension>  
    <Extension Name="IMAGE (EMF Portrait)" Type="Microsoft.ReportingServices.Rendering.ImageRenderer.ImageRenderer,Microsoft.ReportingServices.ImageRendering">  
        <OverrideNames>  
            <Name Language="en-US">EMF in Portait Mode</Name>  
        </OverrideNames>  
        <Configuration>  
            <DeviceInfo>  
                <OutputFormat>EMF</OutputFormat>  
                <PageHeight>11in</PageHeight>  
                <PageWidth>8.5in</PageWidth>  
            </DeviceInfo>  
        </Configuration>  
    </Extension>  
</Render>  
```  
  
## <a name="see-also"></a>請參閱＜  
 [RsReportServer.config 組態檔](../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [RSReportDesigner 組態檔](../reporting-services/report-server/rsreportdesigner-configuration-file.md)   
 [CSV 裝置資訊設定](../reporting-services/csv-device-information-settings.md)   
 [Excel 裝置資訊設定](../reporting-services/excel-device-information-settings.md)   
 [HTML 裝置資訊設定](../reporting-services/html-device-information-settings.md)   
 [影像裝置資訊設定](../reporting-services/image-device-information-settings.md)   
 [MHTML 裝置資訊設定](../reporting-services/mhtml-device-information-settings.md)   
 [PDF 裝置資訊設定](../reporting-services/pdf-device-information-settings.md)   
 [XML 裝置資訊設定](../reporting-services/xml-device-information-settings.md)  
  
  
