---
title: 在 Web 應用程式中使用 SOAP API
description: 您可以透過 Reporting Services SOAP API 存取報表伺服器的完整功能。
ms.date: 06/26/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.custom: seo-lt-2019
ms.topic: reference
helpviewer_keywords:
- SOAP [Reporting Services], Web applications
- impersonation [Reporting Services]
- user impersonation [Reporting Services]
- report servers [Reporting Services], SOAP
- Web applications [Reporting Services]
ms.assetid: e8ca4455-0dc3-4741-8872-3636114938ad
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d7ae6c53033d1ea79a58d566bf57d8ed622e8f8d
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "74796825"
---
# <a name="integrating-reporting-services-using-soap---web-application"></a>使用 SOAP 整合 Reporting Services - Web 應用程式
  您可以透過 Reporting Services SOAP API 存取報表伺服器的完整功能。 因為它是一種 Web 服務，所以可以輕易地存取 SOAP API，以提供企業報表功能給自訂商務應用程式。 您可以從 Web 應用程式存取報表伺服器 Web 服務，這與從 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 應用程式存取 SOAP API 非常類似。 使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]，您就可以產生公開報表伺服器 Web 服務的屬性與方法之 Proxy 類別，而且可讓您使用熟悉的基礎結構與工具，建置以 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 技術為基礎的商務應用程式。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表管理功能可以從 Web 應用程式存取，就和從 Windows 應用程式存取一樣簡單。 從 Web 應用程式，您可以從報表伺服器資料庫新增和移除項目、設定項目安全性、修改報表伺服器資料庫項目、管理排程和傳遞等等。  
  
## <a name="enabling-impersonation"></a>啟用模擬  
 設定 Web 應用程式的第一個步驟是從 Web 服務用戶端啟用模擬。 透過模擬，[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 應用程式可以使用它們正在操作的用戶端識別來執行。 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 依賴 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Information Services (IIS) 驗證使用者並將已驗證的 Token 傳遞給 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 應用程式，或者如果無法驗證使用者，請傳遞未驗證的 Token。 不論是哪一種情況，若有啟用模擬，[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 應用程式不論收到哪一個 Token，都會進行模擬。 您可以透過修改用戶端應用程式的 Web.config 檔案，啟用在用戶端上的模擬：  
  
```asp.net  
<!-- Web.config file. -->  
<identity impersonate="true"/>  
```  
  
> [!NOTE]  
>  預設會啟用模擬。  
  
 如需 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 模擬的詳細資訊，請參閱 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK 文件。  
  
## <a name="managing-the-report-server-using-soap-api"></a>使用 SOAP API 管理報表伺服器。  

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

 您也可以使用 Web 應用程式來管理報表伺服器及其內容。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 隨附的報表管理員，是完全使用 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 與 Reporting Services SOAP API 建立的 Web 應用程式範例。 您可以將報表管理員的報表管理功能加入自訂 Web 應用程式。 例如，您可以傳回報表伺服器資料庫中可用報表的清單，並將其顯示在 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] **Listbox** 控制項中，以供您的使用者選擇。 下列程式碼會連接報表伺服器資料庫，並在報表伺服器資料庫中傳回項目的清單。 接著會將可用的報表加入 Listbox 控制項，如此會顯示每個報表的路徑。  

::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"

 您也可以使用 Web 應用程式來管理報表伺服器及其內容。 Web 入口網站 (隨附於 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]) 是 Web 應用程式的範例，它會管理通常使用 Reporting Services 執行的大部分工作。 您可以將入口網站的報表管理功能新增到自訂 Web 應用程式。 例如，您可以傳回報表伺服器資料庫中可用報表的清單，並將其顯示在 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] **Listbox** 控制項中，以供您的使用者選擇。 下列程式碼會連接報表伺服器資料庫，並在報表伺服器資料庫中傳回項目的清單。 接著會將可用的報表加入 Listbox 控制項，如此會顯示每個報表的路徑。  

::: moniker-end
  
```vb  
Private Sub Page_Load(sender As Object, e As System.EventArgs)  
   ' Create a Web service proxy object and set credentials  
   Dim rs As New ReportingService2005()  
   rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
  
   ' Return a list of catalog items in the report server database  
   Dim items As CatalogItem() = rs.ListChildren("/", True)  
  
   ' For each report, display the path of the report in a Listbox  
   Dim ci As CatalogItem  
   For Each ci In  items  
      If ci.Type = ItemTypeEnum.Report Then  
         catalogListBox.Items.Add(ci.Path)  
      End If  
   Next ci  
End Sub ' Page_Load   
```  
  
```csharp  
private void Page_Load(object sender, System.EventArgs e)  
{  
   // Create a Web service proxy object and set credentials  
   ReportingService2005 rs = new ReportingService2005();  
   rs.Credentials = System.Net.CredentialCache.DefaultCredentials;  
  
   // Return a list of catalog items in the report server database  
   CatalogItem[] items = rs.ListChildren("/", true);  
  
   // For each report, display the path of the report in a Listbox  
   foreach(CatalogItem ci in items)  
   {  
      if (ci.Type == ItemTypeEnum.Report)  
         catalogListBox.Items.Add(ci.Path);  
   }  
}  
```  
  
## <a name="see-also"></a>另請參閱  

 [使用 Web 服務和 .NET Framework 建置應用程式](../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [將 Reporting Services 整合到應用程式](../../reporting-services/application-integration/integrating-reporting-services-into-applications.md)   
 [在 Windows 應用程式中使用 SOAP API](../../reporting-services/application-integration/integrating-reporting-services-using-soap-windows-application.md)  
  
  
