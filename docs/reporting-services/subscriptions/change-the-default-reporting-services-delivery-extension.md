---
title: 變更預設 Reporting Services 傳遞延伸模組 | Microsoft Docs
ms.date: 03/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: subscriptions
ms.topic: conceptual
helpviewer_keywords:
- Report Manager [Reporting Services], default delivery extension
ms.assetid: 5f6fee72-01bf-4f6c-85d2-7863c46c136b
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 007427739f91a12ea6603bbf58450821d2c999ea
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "66500396"
---
# <a name="change-the-default-reporting-services-delivery-extension"></a>變更預設 Reporting Services 傳遞延伸模組
  您可以修改 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態設定，以變更訂閱定義頁面的 **[傳遞者]** 清單中所顯示的預設傳遞延伸模組。 例如，您可以修改組態，使得在使用者建立新的訂閱時依預設會選取檔案共用傳遞，而不是電子郵件傳遞。 您也可以變更傳遞延伸模組在使用者介面中列出的順序。  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式 | [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 包含電子郵件和 Windows 檔案共用傳遞延伸模組。 如果您部署了自訂或協力廠商延伸模組來支援自訂傳遞，那麼報表伺服器可能會有其他的傳遞延伸模組。 傳遞延伸模組是否可用取決於該模組是否部署於報表伺服器。  
  
## <a name="default-native-mode-report-server-configuration"></a>預設原生模式報表伺服器組態  
 在 **[傳遞者]** 清單的 [報表管理員] 中顯示傳遞延伸模組的順序，是根據 **RSReportServer.config** 檔中傳遞延伸模組項目的順序而定。 例如，下圖在清單中會先顯示電子郵件，並依預設加以選取。  
  
 ![預設的傳遞延伸模組清單](../../reporting-services/subscriptions/media/ssrs-default-delivery.png "預設的傳遞延伸模組清單")  
  
 以下是 **RSReportServer.config** 的預設區段，會控制預設傳遞延伸模組及其在報表管理員中的顯示順序。 請注意，電子郵件會先出現在檔案中，並且設為預設值。  
  
```  
<DeliveryUI>  
     <Extension Name="Report Server Email" Type="Microsoft.ReportingServices.EmailDeliveryProvider.EmailDeliveryProviderControl,ReportingServicesEmailDeliveryProvider">  
          <DefaultDeliveryExtension>True</DefaultDeliveryExtension>  
               <Configuration>  
               <RSEmailDPConfiguration>  
                    <DefaultRenderingExtension>MHTML</DefaultRenderingExtension>  
               </RSEmailDPConfiguration>  
               </Configuration>  
     </Extension>  
     <Extension Name="Report Server FileShare" Type="Microsoft.ReportingServices.FileShareDeliveryProvider.FileShareUIControl,ReportingServicesFileShareDeliveryProvider"/>  
</DeliveryUI>  
```  
  
#### <a name="configure-file-share-delivery-as-the-default-delivery-extension-in-report-manager"></a>將檔案共用傳遞設定為報表管理員中的預設傳遞延伸模組  
  
1.  此程序中的步驟會修改組態，讓檔案共用傳遞列示為 UI 中的第一個選項，並且是預設選取項目。  
  
     在文字編輯器中開啟 RSReportServer.config 檔。 如需組態檔的詳細資訊，請參閱 [RsReportServer.config 組態檔](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)。 組態變更之後，UI 會如下圖所示：  
  
     ![修改過的傳遞延伸模組清單](../../reporting-services/subscriptions/media/ssrs-modified-delivery.png "修改過的傳遞延伸模組清單")  
  
2.  修改 DeliveryUI 區段使其如下列範例所示，並記下主要變更：  
  
    1.  FileShare 延伸模組位於電子郵件延伸模組之前。 這會變更延伸模組在報表管理員中的列出順序。  
  
    2.  檔案共用延伸模組包含 DefaultExtension 標記 `<DefaultDeliveryExtension>True</DefaultDeliveryExtension>` ，且延伸模組結束標記已加上 `</Extension>`。  
  
    3.  電子郵件延伸模組不再設定為預設值。 `<DefaultDeliveryExtension>False</DefaultDeliveryExtension>`  
  
    ```  
    <DeliveryUI>  
         <Extension Name="Report Server FileShare" Type="Microsoft.ReportingServices.FileShareDeliveryProvider.FileShareUIControl,ReportingServicesFileShareDeliveryProvider">  
              <DefaultDeliveryExtension>True</DefaultDeliveryExtension>  
         </Extension>  
         <Extension Name="Report Server Email" Type="Microsoft.ReportingServices.EmailDeliveryProvider.EmailDeliveryProviderControl,ReportingServicesEmailDeliveryProvider">  
         <DefaultDeliveryExtension>False</DefaultDeliveryExtension>  
         <Configuration>  
              <RSEmailDPConfiguration>  
                   <DefaultRenderingExtension>MHTML</DefaultRenderingExtension>  
              </RSEmailDPConfiguration>  
         </Configuration>  
         </Extension>  
    </DeliveryUI>  
    ```  
  
3.  儲存組態檔。  
  
4.  在幾分鐘內，報表伺服器即會重新載入組態檔，且新設定將會生效。 您可以重新啟動報表伺服器服務，以強制載入組態檔。  
  
     在讀取組態時，下列事件會寫入至 Windows 事件記錄檔。  
  
     **事件識別碼：** 109  
  
     **來源：** 報表伺服器 Windows 服務 (執行個體名稱)  
  
     已修改 RSReportServer.config 檔  
  
## <a name="sharepoint-mode-report-servers"></a>SharePoint 模式報表伺服器  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式會在 SharePoint 服務應用程式資料庫中儲存延伸模組資訊，而不是在 RsrReportServer.config 檔中儲存。 在 SharePoint 模式中，傳遞延伸模組組態會使用 PowerShell 進行修改。  
  
#### <a name="configure-the-default-delivery-extension"></a>設定預設傳遞延伸模組  
  
1.  開啟 **[SharePoint 管理命令介面]** 。  
  
2.  如果您已知道 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式的名稱，您可以略過此步驟。 使用下列 PowerShell，列出您 SharePoint 伺服器陣列中的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式。  
  
    ```  
    get-sprsserviceapplication | format-list *  
    ```  
  
3.  執行下列 PowerShell，以驗證 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式 "ssrsapp" 目前的預設傳遞延伸模組。  
  
    ```  
    $app=get-sprsserviceapplication | where {$_.name -like "ssrsapp*"};Get-SPRSExtension -identity $app | where{$_.ServerDirectivesXML -like "<DefaultDelivery*"} | format-list *  
  
    ```
  
## <a name="see-also"></a>另請參閱  
 [RsReportServer.config 組態檔](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [RsReportServer.config 組態檔](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Reporting Services 中的檔案共用傳遞](../../reporting-services/subscriptions/file-share-delivery-in-reporting-services.md)   
 [Reporting Services 中的電子郵件傳遞](../../reporting-services/subscriptions/e-mail-delivery-in-reporting-services.md)   

