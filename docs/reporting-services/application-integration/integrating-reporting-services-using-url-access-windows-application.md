---
title: "在 Windows 應用程式中使用 URL 存取 |Microsoft 文件"
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
- Windows applications [Reporting Services]
- Web Browser controls [Reporting Services]
- Windows Forms [Reporting Services]
- browser controls [Reporting Services]
- URL access [Reporting Services], Windows applications
ms.assetid: a4b222e5-0cbd-409c-92c4-046a674db8ac
caps.latest.revision: 48
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 6174bfd45317faf9b6c8c7131dd1c5026d3a4d51
ms.contentlocale: zh-tw
ms.lasthandoff: 06/13/2017

---
# <a name="integrating-reporting-services-using-url-access---windows-application"></a>使用 URL 存取的 Windows 應用程式整合 Reporting Services
  雖然會為 Web 環境最佳化報表伺服器的 URL 存取，不過，您也可以使用 URL 存取來將 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表內嵌到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 應用程式。 不過，需要 Windows Form 的 URL 存取仍然需要您使用網頁瀏覽器技術。 您可以透過 URL 存取與 Windows Form 使用下列整合案例：  
  
-   透過以程式設計方式啟動網頁瀏覽器，來顯示 Windows Form 應用程式中的報表。  
  
-   使用 Windows Form 上的 <xref:System.Windows.Forms.WebBrowser> 控制項顯示報表。  
  
## <a name="starting-internet-explorer-from-a-windows-form"></a>從 Windows Form 啟動 Internet Explorer  
 您可以使用 <xref:System.Diagnostics.Process> 類別來存取正在電腦上執行的處理序。 <xref:System.Diagnostics.Process>類別就很有用[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]建構來啟動、 停止、 控制和監視應用程式。 若要檢視您的報表伺服器資料庫中的特定報表，您可以啟動**IExplore**程序，在 URL 中傳遞報表。 下列程式碼範例可用以啟動 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Explorer，並在使用者按一下 Windows Form 上的按鈕時，傳遞特定的報表 URL。  
  
```vb  
Private Sub viewReportButton_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles viewReportButton.Click  
   ' Build the URL access string based on values supplied by a user  
   Dim url As String = serverUrlTextBox.Text + "?" & reportPathTextBox.Text & _  
   "&rs:Command=Render" & "&rs:Format=HTML4.0"  
  
   ' If the user does not select the toolbar check box,  
   ' turn the toolbar off in the HTML Viewer  
   If toolbarCheckBox.Checked = False Then  
      url += "&rc:Toolbar=False"  
   End If  
   ' load report in the Web browser  
   Try  
      System.Diagnostics.Process.Start("IExplore", url)  
   Catch  
      MessageBox.Show("The system could not start the specified report using Internet Explorer.", _  
      "An error has occurred", MessageBoxButtons.OK, MessageBoxIcon.Error)  
   End Try  
End Sub 'viewReportButton_Click  
```  
  
```csharp  
// Sample click event for a Button control on a Windows Form  
private void viewReportButton_Click(object sender, System.EventArgs e)  
{  
   // Build the URL access string based on values supplied by a user  
   string url = serverUrlTextBox.Text + "?" + reportPathTextBox.Text +  
      "&rs:Command=Render" + "&rs:Format=HTML4.0";  
  
   // If the user does not check the toolbar check box,  
   // turn the toolbar off in the HTML Viewer  
   if (toolbarCheckBox.Checked == false)  
      url += "&rc:Toolbar=False";  
  
   // load report in the Web browser  
   try  
   {  
      System.Diagnostics.Process.Start("IExplore", url);  
   }  
  
   catch (Exception)  
   {  
      MessageBox.Show(  
         "The system could not open the specified report using Internet Explorer.",   
         "An error has occurred", MessageBoxButtons.OK, MessageBoxIcon.Error);  
   }  
}  
```  
  
## <a name="embedding-a-browser-control-on-a-windows-form"></a>在 Windows Form 上內嵌瀏覽器控制項  
 如果您不想在外部網頁瀏覽器中檢視報表，可以使用 <xref:System.Windows.Forms.WebBrowser> 控制項將網頁瀏覽器緊密地內嵌成為 Windows Form 的一部分。  
  
###### <a name="to-add-the-webbrowser-control-to-your-windows-form"></a>將 WebBrowser 控制項加入 Windows Form  
  
1.  建立新的 Windows 應用程式在[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[csprcs](../../includes/csprcs-md.md)]或[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]。  
  
2.  找出<xref:System.Windows.Forms.WebBrowser>控制**工具箱** 對話方塊。  
  
     如果**工具箱**是看不到您可以存取它，即可**檢視**功能表項目，然後選取**工具箱**。  
  
3.  拖曳<xref:System.Windows.Forms.WebBrowser>控制項拖曳到您的 Windows Form 的設計介面。  
  
     <xref:System.Windows.Forms.WebBrowser>名為 webBrowser1 的控制項加入至表單  
  
 您直接<xref:System.Windows.Forms.WebBrowser>藉由呼叫的 URL 來控制其**瀏覽**方法。 您可以在執行階段將特定的 URL 存取字串指派到 <xref:System.Windows.Forms.WebBrowser> 控制項，如下列範例所示。  
  
```vb  
Dim url As String = "http://localhost/reportserver?/" & _  
                    "AdventureWorks2012 Sample Reports/" & _  
                    "Company Sales&rs:Command=Render"  
WebBrowser1.Navigate(url)  
```  
  
```csharp  
string url = "http://localhost/reportserver?/" +  
             "AdventureWorks2012 Sample Reports/" +  
             "Company Sales&rs:Command=Render";  
webBrowser1.Navigate(url);  
```  
  
## <a name="see-also"></a>另請參閱  
 [將 Reporting Services 整合到應用程式](../../reporting-services/application-integration/integrating-reporting-services-into-applications.md)   
 [使用 URL 存取整合 Reporting Services](../../reporting-services/application-integration/integrating-reporting-services-using-url-access.md)   
 [使用 SOAP 整合 Reporting Services](../../reporting-services/application-integration/integrating-reporting-services-using-soap.md)   
 [使用 ReportViewer 控制項整合 Reporting Services](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls.md)   
 [URL 存取 &#40;SSRS &#41;](../../reporting-services/url-access-ssrs.md)  
  
  
