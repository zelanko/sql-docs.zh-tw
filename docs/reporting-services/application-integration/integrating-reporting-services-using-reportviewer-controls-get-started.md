---
title: "開始使用 ReportViewer 2016 控制項 | Microsoft Docs"
ms.custom: 
ms.date: 06/12/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: application-integration
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 01a821c4-2920-400c-be03-93d26c749bb1
caps.latest.revision: "12"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Active
ms.openlocfilehash: 9b177bb647fd1c9daf5fb330f3bff15cf3e73ab3
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2018
---
# <a name="integrating-reporting-services-using-reportviewer-controls---get-started"></a>使用 ReportViewer 控制項整合 Reporting Services - 快速入門

了解開發人員如何透過 Reporting Services 2016 ReportViewer 控制項，內嵌 ASP.NET 網站的分頁報表以及 Windows Forms 應用程式。 您可以將控制項新增至新的專案，或更新現有的專案。

## <a name="adding-the-reportviewer-control-to-a-new-web-project"></a>將 ReportViewer 控制項新增至新的 Web 專案

1. 建立新的 **ASP.NET 空網站**或開啟現有的 ASP.NET 專案。

    ![ssRS-Create-New-ASPNET-Project](../../reporting-services/application-integration/media/ssrs-create-new-aspnet-project.png)

2. 透過 **Nuget 套件管理員主控台**安裝 ReportViewer 2016 控制項 Nuget 套件。

    ```
    Install-Package Microsoft.ReportingServices.ReportViewerControl.WebForms
    ```
3. 在專案中新增新的 .aspx 頁面，並註冊 ReportViewer 控制項組件供頁面使用。

    ```
    <%@ Register assembly="Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" namespace="Microsoft.Reporting.WebForms" tagprefix="rsweb" %>
    ```
    
4. 將 **ScriptManagerControl** 新增至頁面。

5. 將 ReportViewer 控制項新增至頁面。 您可以更新以下程式碼片段，以參考遠端報表伺服器上裝載的報表。

    ```
    <rsweb:ReportViewer ID="ReportViewer1" runat="server" ProcessingMode="Remote">
      <ServerReport ReportPath="" ReportServerUrl="" />
    </rsweb:ReportViewer>
    ```
    
最後的頁面應該類似下例。

```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs" Inherits="Sample" %>

<%@ Register assembly="Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" namespace="Microsoft.Reporting.WebForms" tagprefix="rsweb" %>

<!DOCTYPE html>

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <meta http-equiv="X-UA-Compatible" content="IE=edge" /> 
    <title></title>
</head>
<body>
    <form id="form1" runat="server">
    <asp:ScriptManager runat="server"></asp:ScriptManager>        
        <rsweb:ReportViewer ID="ReportViewer1" runat="server" ProcessingMode="Remote">
            <ServerReport ReportServerUrl="http://AContosoDepartment/ReportServer" ReportPath="/LatestSales" />
        </rsweb:ReportViewer>
    </form>
</body>
</html>

```

## <a name="updating-an-existing-project-to-use-the-reportviewer-control"></a>更新現有的專案以使用 ReportViewer 控制項

若要在現有的專案中使用 ReportViewer 2016 控制項，請透過 Nuget 新增控制項並更新版本 *14.0.0.0* 的組件參考。 這包括更新專案的 web.config 和所有參考 ReportViewer 控制項的 .aspx 頁面。

### <a name="sample-webconfig-changes"></a>範例 web.config 變更

```
<?xml version="1.0"?>
<!--
  For more information on how to configure your ASP.NET application, please visit
  http://go.microsoft.com/fwlink/?LinkId=169433
  -->
<configuration>
  <system.web>
    <compilation debug="true" targetFramework="4.5.2">
      <assemblies>
        <!-- All assemblies updated to version 14.0.0.0. -->
        <add assembly="Microsoft.ReportViewer.Common, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.DataVisualization, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.Design, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.ProcessingObjectModel, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.WebDesign, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.WinForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
      </assemblies>
      <buildProviders>
        <!-- Version updated to 14.0.0.0. -->
        <add extension=".rdlc"
          type="Microsoft.Reporting.RdlBuildProvider, Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
      </buildProviders>
    </compilation>
    <httpRuntime targetFramework="4.5.2"/>
    <httpHandlers>
      <!-- Version updated to 14.0.0.0 -->
      <add path="Reserved.ReportViewerWebControl.axd" verb="*"
        type="Microsoft.Reporting.WebForms.HttpHandler, Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"
        validate="false"/>
    </httpHandlers>
  </system.web>
  <system.webServer>
    <validation validateIntegratedModeConfiguration="false"/>
    <modules runAllManagedModulesForAllRequests="true"/>
    <handlers>
      <!-- Version updated to 14.0.0.0 -->
      <add name="ReportViewerWebControlHandler" verb="*" path="Reserved.ReportViewerWebControl.axd" preCondition="integratedMode"
        type="Microsoft.Reporting.WebForms.HttpHandler, Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
    </handlers>
  </system.webServer>
</configuration>
```

### <a name="sample-aspx"></a>範例 .aspx

```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs" Inherits="SampleAspx" %>

<!-- Update version to 14.0.0.0 -->
<%@ Register assembly="Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" namespace="Microsoft.Reporting.WebForms" tagprefix="rsweb" %>

<!DOCTYPE html>
```

## <a name="adding-the-reportviewer-control-to-a-new-windows-forms-project"></a>將 ReportViewer 控制項新增至新的 Windows Forms 專案

1. 建立新的 **Windows Forms 應用程式** 或開啟現有的專案。

    ![ssRS-Create-New-winforms-Project](../../reporting-services/application-integration/media/ssrs-create-new-winforms-project.png)

2. 透過 **Nuget 套件管理員主控台**安裝 ReportViewer 2016 控制項 Nuget 套件。

    ```
    Install-Package Microsoft.ReportingServices.ReportViewerControl.WinForms
    ```
3. 從程式碼新增新的控制項，或[將控制項新增至 [工具箱]](##adding-control-to-visual-studio-toolbar)。

    ```
    private Microsoft.Reporting.WinForms.ReportViewer reportViewer1;
    
    private void InitializeComponent()
    {
        this.reportViewer1 = new Microsoft.Reporting.WinForms.ReportViewer();
        this.SuspendLayout();
        // 
        // reportViewer1
        // 
        this.reportViewer1.Location = new System.Drawing.Point(168, 132);
        this.reportViewer1.Name = "reportViewer1";
        this.reportViewer1.ServerReport.BearerToken = null;
        this.reportViewer1.Size = new System.Drawing.Size(396, 246);
        this.reportViewer1.TabIndex = 0;
        // 
        // Form1
        // 
        this.Controls.Add(this.reportViewer1);
    }
    ```

## <a name="how-to-set-100-height-on-the-report-viewer-2016-control"></a>如何在報表檢視器 2016 控制項上設定 100% 的高度

新的報表檢視器 2016 控制項已針對 HTML5 標準模式頁面最佳化，適用於所有現代化瀏覽器。 過去使用舊的 RVC 控制項，當您設定 100 % 高度屬性時，即使沒有任何上階指定高度，它都會作用。 此行為在 HTML5 中已變更。 當您在新的 RVC 控制項上設定此屬性時，它只有在父項目有定義的高度 (亦即不是自動值)，或所有上階的 RVC 也有 100% 高度時，才會正確運作。

以下為兩個示範範例。

### <a name="by-setting-the-height-of-all-the-parent-elements-to-100"></a>將所有父項目的高度設為 100%

```
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <style>
        html,body,form,#div1 {
            height: 100%; 
        }
    </style>
   </head>
<body>
    <form id="form1" runat="server">
    <div id="div1" >
            <asp:ScriptManager runat="server"></asp:ScriptManager>
        <rsweb:ReportViewer ID="ReportViewer1" runat="server" ProcessingMode="Remote" Height="100%" Width="100%">
            <ServerReport ReportServerUrl="http://test/ReportServer" ReportPath="/testreport" />
        </rsweb:ReportViewer>
    </div>
    </form>
</body>
</html>

```

### <a name="by-setting-the-style-height-attribute-on-the-parent-of-the-reportviewer-control"></a>設定 reportviewer 控制項的父代樣式高度屬性

如需檢視區百分比長度的詳細資訊，請參閱 [Viewport-percentage lengths](https://www.w3.org/TR/css3-values/#viewport-relative-lengths) (檢視區百分比長度)。

```
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
</head>
<body>
    <form id="form1" runat="server">
    <div style="height:100vh;">
            <asp:ScriptManager runat="server"></asp:ScriptManager>
        <rsweb:ReportViewer ID="ReportViewer1" runat="server" ProcessingMode="Remote" Height="100%" Width="100%">
            <ServerReport ReportServerUrl="http://test/ReportServer" ReportPath="/testreport" />
        </rsweb:ReportViewer>
    </div>
    </form>
</body>
</html>

```

## <a name="adding-control-to-visual-studio-toolbar"></a>將控制項新增至 Visual Studio 工具列

報表檢視器控制項現在隨附為 Nuget 套件。 因為這個緣故，Visual Studio 工具箱中預設不顯示報表檢視器控制項。 您可以執行下列動作，將控制項新增至工具箱。

1. 依上述指示安裝 WinForms 或 WebForms 的 Nuget 套件。

2. 移除 [工具箱] 中列出的 ReportViewer 控制項。 這是 12.x 版的控制項。

    ![ssRS-remove-old-rvcontrol-toolbox](../../reporting-services/application-integration/media/ssrs-remove-old-rvcontrol-toolbox.png)

3. 以滑鼠右鍵按一下 [工具箱] 的任何位置，然後選取 [選擇項目]。

    ![ssRS-toolbox-choose-item](../../reporting-services/application-integration/media/ssrs-toolbox-choose-item.png)
    
4. 在 [.NET Framework 元件] 中選取 [瀏覽]。

    ![ssRS-toolbox-browse](../../reporting-services/application-integration/media/ssrs-toolbox-browse.png)

5. 從安裝的 Nuget 套件中選取 **Microsoft.ReportViewer.WinForms.dll** 或 **Microsoft.ReportViewer.WebForms.dll**。

    > [!NOTE] 
    > Nuget 套件會安裝在專案的解決方案目錄中。 dll 的路徑類似：`{Solution Directory}\packages\Microsoft.ReportingServices.ReportViewerControl.Winforms.{version}\lib\net40` 或 `{Solution Directory}\packages\Microsoft.ReportingServices.ReportViewerControl.WebForms.{version}\lib\net40`。

6. 新的控制項應該顯示在 [工具箱] 中。 如希望，您可以將它移動至工具箱的另一個索引標籤中。

    ![ssRS-toolbox-rvcontrol](../../reporting-services/application-integration/media/ssrs-toolbox-rvcontrol.png)

### <a name="things-to-be-aware-of"></a>注意事項

- 這會在目前的專案中新增已安裝 Nuget 套件的參考。 [工具箱] 中的項目會保存至其他專案。 當您在新的解決方案/專案中安裝 Nuget 套件時，工具箱項目可能會參考較舊的版本。 

- 即使組件無法再使用，[工具箱] 中仍保留控制項。 若已刪除該專案，當您嘗試從 [工具箱] 新增控制項時，Visual Studio 會擲回錯誤。 若要更正這個錯誤，請從 [工具箱] 移除控制項，使用上述步驟重新新增它。


## <a name="common-issues"></a>常見的問題
    
- ReportViewer 2016 控制項旨在搭配新式瀏覽器使用。 如果瀏覽器以 IE 相容性模式呈現網頁，控制項可能無法運作。 內部網路網站可能需要中繼標籤覆寫設定，這會鼓勵以相容性模式轉譯內部網路頁面。

    ```
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    ```
      
## <a name="providing-feedback"></a>提供意見反應

在 [Reporting Services MSDN 論壇](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=sqlreportingservices)或透過電子郵件 [RVCFeedback@microsoft.com](mailto:RVCFeedback@microsoft.com)，讓小組了解您遇到的控制項問題。

## <a name="see-also"></a>另請參閱

[2016 ReportingViewer 控制項中的資料收集](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls-data-collection.md)  
更多問題嗎？ [試試 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)

