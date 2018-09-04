---
title: 在 Windows 應用程式中使用 SOAP API | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.suite: pro-bi
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- rendered reports [Reporting Services]
- Windows applications [Reporting Services]
- Windows Forms [Reporting Services]
- SOAP [Reporting Services], Windows applications
ms.assetid: e4804792-20cd-4df2-9257-fb958ff447b4
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9e3337d0912e0249c7ac49523bb4159458ba36e8
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2018
ms.locfileid: "43274045"
---
# <a name="integrating-reporting-services-using-soap---windows-application"></a>使用 SOAP 整合 Reporting Services - Windows 應用程式
  您可以透過 Reporting Services SOAP API 存取報表伺服器的完整功能。 SOAP API 是一種 Web 服務，因此可以輕易地存取，以提供企業報表功能給自訂商務應用程式。 您只要撰寫呼叫服務的程式碼，即可在 Windows 應用程式中存取 Web 服務。 使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]，您就可以產生公開 Web 服務的屬性與方法之 Proxy 類別，而且可讓您使用熟悉的基礎結構與工具，建立以 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 技術為基礎的商務應用程式。  
  
## <a name="integrating-report-management-functionality-using-windows-forms"></a>使用 Windows Form 整合報表管理功能  
 與 URL 存取不同的是，SOAP API 會公開一組透過報表伺服器取得的完整管理功能。 這表示報表管理員的整個系統管理功能，是透過 SOAP 提供給開發人員使用。 因此，您可以使用 Windows Form 開發完整的管理工具。 例如，在 Windows 應用程式中，您可以讓使用者擷取報表伺服器命名空間的內容。 若要這樣做，您可以使用 Web 服務的 <xref:ReportService2010.ReportingService2010.ListChildren%2A> 方法，列出報表伺服器資料庫中的所有項目，然後使用 Listview、Treeview 或 Combobox 控制項來對使用者顯示這些項目。 下列 Web 服務程式碼可用於當使用者按一下表單上的按鈕時，擷取使用者的 [我的報表] 資料夾中可用報表的目前清單：  
  
```vb  
' Button click event that retrieves a list of reports from  
' the My Reports folder and displays them in a combo box  
Private Sub listReportsButton_Click(sender As Object, e As System.EventArgs)  
   ' Create a new Web service object and set credentials  
   ' to Windows Authentication  
   Dim rs As New ReportingService2010()  
   rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
  
   ' Return the list of items in My Reports  
   Dim items As CatalogItem() = rs.ListChildren("/Adventureworks 2008 Sample Reports", False)  
  
   Dim ci As CatalogItem  
   For Each ci In  items  
      ' If the item is a report, add it to   
      ' a combo box  
      If ci.TypeName = "Report" Then  
         catalogComboBox.Items.Add(ci.Name)  
      End If  
   Next ci  
End Sub 'listReportsButton_Click  
```  
  
```csharp  
// Button click event that retrieves a list of reports from  
// the My Reports folder and displays them in a combo box  
private void listReportsButton_Click(object sender, System.EventArgs e)  
{  
   // Create a new Web service object and set credentials  
   // to Windows Authentication  
   ReportingService2010 rs = new ReportingService2010();  
   rs.Credentials = System.Net.CredentialCache.DefaultCredentials;  
  
   // Return the list of items in My Reports  
   CatalogItem[] items = rs.ListChildren("/Adventureworks 2008 Sample Reports", false);  
  
   foreach (CatalogItem ci in items)  
   {  
      // If the item is a report, add it to   
      // a combo box  
      if (ci.TypeName == "Report")  
         catalogComboBox.Items.Add(ci.Name);  
   }  
}  
```  
  
 從這裡，您可以讓使用者從下拉式方塊選取報表，並使用網頁瀏覽器控制項或是影像控制項來預覽表單上的報表。  
  
## <a name="enabling-report-viewing-and-navigation-using-windows-forms"></a>使用 Windows Form 啟用報表檢視與導覽  
 將報表整合到 Windows Form 應用程式有兩種方法。  
  
 您可以使用 SOAP API 將報表轉譯成任何使用 <xref:ReportExecution2005.ReportExecutionService.Render%2A> 方法的支援轉譯格式。 透過 SOAP 啟用報表檢視與導覽有些輕微的缺點：  
  
-   您無法透過 URL 存取利用 HTML 檢視器隨附的報表工具列之內建功能。  
  
-   如果您轉譯為 HTML，必須使用 <xref:ReportExecution2005.ReportExecutionService.RenderStream%2A> 方法，將任何影像或是資源個別轉譯為其他的資料流。  
  
-   比起 SOAP API，使用 URL 存取來轉譯報表具有些許效能優點。  
  
 不過，您可以用程式設計方式使用 SOAP API 的 <xref:ReportExecution2005.ReportExecutionService.Render%2A> 方法來轉譯報表，並將它們儲存為各個輸出格式。 這個優點勝過需要使用者互動的 URL 存取。 當您使用 SOAP API <xref:ReportExecution2005.ReportExecutionService.Render%2A> 方法轉譯報表時，可以轉譯為任何支援的輸出格式。  
  
 您也可以使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)] 隨附且任意散發的 ReportViewer 控制項。 ReportViewer 控制項可輕鬆地將 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 功能內嵌至自訂應用程式。 ReportViewer 控制項主要是供開發人員使用，他們想要提供預先設計、完整撰寫的報表作為應用程式功能集的一部份 (例如，網站管理應用程式可能包含在公司網站上顯示點選流向分析的報表)。 將控制項內嵌在應用程式中，是將 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 伺服器元件包含在應用程式部署中的簡化替代方案。 控制項雖然提供報表功能，但沒有您在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中所看到的其他報表撰寫、發行或散發和傳遞支援。  
  
 ReportViewer 控制項有兩個版本，一個用於豐富的 Windows 用戶端應用程式，一個用於 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 應用程式。 控制項同時支援本機處理和遠端處理模式。 在本機處理模式中，應用程式提供報表定義和資料集以及觸發程序報表處理。 在遠端處理模式中，資料擷取和報表處理是在報表伺服器上進行，而控制項則是用於顯示和報表導覽。 這個模式可讓您建立豐富的應用程式，其範圍從桌上型到企業型都有。  
  
 ReportViewer 控制項的相關資訊記載於 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 線上說明中。 如需詳細資訊，請參閱 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 產品文件集。  
  
## <a name="see-also"></a>另請參閱  
 [使用 Web 服務和 .NET Framework 建置應用程式](../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [將 Reporting Services 整合到應用程式](../../reporting-services/application-integration/integrating-reporting-services-into-applications.md)   
 [在 Web 應用程式中使用 SOAP API](../../reporting-services/application-integration/integrating-reporting-services-using-soap-web-application.md)  
  
  
