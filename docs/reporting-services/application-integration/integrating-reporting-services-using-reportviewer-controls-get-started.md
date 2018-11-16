---
title: 開始使用 ReportViewer 2016 控制項 | Microsoft Docs
ms.date: 09/18/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: application-integration
ms.topic: conceptual
ms.assetid: 01a821c4-2920-400c-be03-93d26c749bb1
author: markingmyname
ms.author: maghan
ms.openlocfilehash: fedc2265a7d8e879a2ca67c5d2e6946ae1cb2c30
ms.sourcegitcommit: 9ece10c2970a4f0812647149d3de2c6b75713e14
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/16/2018
ms.locfileid: "51812242"
---
# <a name="integrating-reporting-services-using-the-report-viewer-controls---get-started"></a>使用報表檢視器控制項整合 Reporting Services - 入門

報表檢視器控制項可以用來將 Reporting Services RDL 報表整合到 WebForms 和 WinForms 應用程式。 如需最新更新的詳細資料，請參閱[變更記錄](changelog.md)。

## <a name="adding-the-report-viewer-control-to-a-new-web-project"></a>將報表檢視器控制項新增至新的 Web 專案

1. 建立新的 **ASP.NET 空網站**或開啟現有的 ASP.NET 專案。

    ![ssRS-Create-New-ASPNET-Project](../../reporting-services/application-integration/media/ssrs-create-new-aspnet-project.png)

2. 透過 **Nuget 套件管理員主控台**安裝報表檢視器控制項 Nuget 套件。

    ```
    Install-Package Microsoft.ReportingServices.ReportViewerControl.WebForms
    ```
3. 在專案中新增新的 .aspx 頁面，並註冊報表檢視器控制項組件供頁面使用。

    ```
    <%@ Register assembly="Microsoft.ReportViewer.WebForms, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" namespace="Microsoft.Reporting.WebForms" tagprefix="rsweb" %>
    ```
    
4. 將 **ScriptManagerControl** 新增至頁面。

5. 將報表檢視器控制項新增至頁面。 您可以更新以下程式碼片段，以參考遠端報表伺服器上裝載的報表。

    ```
    <rsweb:ReportViewer ID="ReportViewer1" runat="server" ProcessingMode="Remote">
      <ServerReport ReportPath="" ReportServerUrl="" />
    </rsweb:ReportViewer>
    ```
    
最後的頁面應該類似下例。

```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs" Inherits="Sample" %>

<%@ Register assembly="Microsoft.ReportViewer.WebForms, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" namespace="Microsoft.Reporting.WebForms" tagprefix="rsweb" %>

<!DOCTYPE html>

<html xmlns="https://www.w3.org/1999/xhtml">
<head runat="server">
    <meta http-equiv="X-UA-Compatible" content="IE=edge" /> 
    <title></title>
</head>
<body>
    <form id="form1" runat="server">
    <asp:ScriptManager runat="server"></asp:ScriptManager>        
        <rsweb:ReportViewer ID="ReportViewer1" runat="server" ProcessingMode="Remote">
            <ServerReport ReportServerUrl="https://AContosoDepartment/ReportServer" ReportPath="/LatestSales" />
        </rsweb:ReportViewer>
    </form>
</body>
</html>

```

## <a name="updating-an-existing-project-to-use-the-report-viewer-control"></a>更新現有的專案以使用報表檢視器控制項

請務必更新版本 *15.0.0.0* 的任何組件參考 (包含專案的 web.config 以及參考檢視器控制項的所有 .aspx 頁面)。

### <a name="sample-webconfig-changes"></a>範例 web.config 變更

```
<?xml version="1.0"?>
<!--
  For more information on how to configure your ASP.NET application, please visit
  https://go.microsoft.com/fwlink/?LinkId=169433
  -->
<configuration>
  <system.web>
    <compilation debug="true" targetFramework="4.5.2">
      <assemblies>
        <!-- All assemblies updated to version 15.0.0.0. -->
        <add assembly="Microsoft.ReportViewer.Common, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.DataVisualization, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.Design, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.ProcessingObjectModel, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.WebDesign, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.WebForms, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.WinForms, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
      </assemblies>
      <buildProviders>
        <!-- Version updated to 15.0.0.0. -->
        <add extension=".rdlc"
          type="Microsoft.Reporting.RdlBuildProvider, Microsoft.ReportViewer.WebForms, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
      </buildProviders>
    </compilation>
    <httpRuntime targetFramework="4.5.2"/>
    <httpHandlers>
      <!-- Version updated to 15.0.0.0 -->
      <add path="Reserved.ReportViewerWebControl.axd" verb="*"
        type="Microsoft.Reporting.WebForms.HttpHandler, Microsoft.ReportViewer.WebForms, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"
        validate="false"/>
    </httpHandlers>
  </system.web>
  <system.webServer>
    <validation validateIntegratedModeConfiguration="false"/>
    <modules runAllManagedModulesForAllRequests="true"/>
    <handlers>
      <!-- Version updated to 15.0.0.0 -->
      <add name="ReportViewerWebControlHandler" verb="*" path="Reserved.ReportViewerWebControl.axd" preCondition="integratedMode"
        type="Microsoft.Reporting.WebForms.HttpHandler, Microsoft.ReportViewer.WebForms, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
    </handlers>
  </system.webServer>
</configuration>
```

### <a name="sample-aspx"></a>範例 .aspx

```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs" Inherits="SampleAspx" %>

<!-- Update version to 15.0.0.0 -->
<%@ Register assembly="Microsoft.ReportViewer.WebForms, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" namespace="Microsoft.Reporting.WebForms" tagprefix="rsweb" %>

<!DOCTYPE html>
```

## <a name="adding-the-report-viewer-control-to-a-new-windows-forms-project"></a>將報表檢視器控制項新增至新的 Windows Forms 專案

1. 建立新的 **Windows Forms 應用程式** 或開啟現有的專案。

    ![ssRS-Create-New-winforms-Project](../../reporting-services/application-integration/media/ssrs-create-new-winforms-project.png)

2. 透過 **Nuget 套件管理員主控台**安裝報表檢視器控制項 Nuget 套件。

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

## <a name="how-to-set-100-height-on-the-report-viewer-control"></a>如何在報表檢視器控制項上設定 100% 的高度

如果將檢視器控制項的高度設定為 100%，則需要父項目具有定義的高度，或需要所有上階都具有高度百分比。

### <a name="setting-the-height-of-all-the-ancestors-to-100"></a>將所有上階的高度設定為 100%

```
<!DOCTYPE html>
<html xmlns="https://www.w3.org/1999/xhtml">
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
            <ServerReport ReportServerUrl="https://test/ReportServer" ReportPath="/testreport" />
        </rsweb:ReportViewer>
    </div>
    </form>
</body>
</html>

```

### <a name="setting-the-parents-height-attribute"></a>設定父代的高度屬性

如需檢視區百分比長度的詳細資訊，請參閱 [Viewport-percentage lengths](https://www.w3.org/TR/css3-values/#viewport-relative-lengths) (檢視區百分比長度)。

```
<!DOCTYPE html>
<html xmlns="https://www.w3.org/1999/xhtml">
<head runat="server">
</head>
<body>
    <form id="form1" runat="server">
    <div style="height:100vh;">
            <asp:ScriptManager runat="server"></asp:ScriptManager>
        <rsweb:ReportViewer ID="ReportViewer1" runat="server" ProcessingMode="Remote" Height="100%" Width="100%">
            <ServerReport ReportServerUrl="https://test/ReportServer" ReportPath="/testreport" />
        </rsweb:ReportViewer>
    </div>
    </form>
</body>
</html>

```

## <a name="adding-control-to-visual-studio-toolbar"></a>將控制項新增至 Visual Studio 工具列

報表檢視器控制項現在隨附為 NuGet 套件，而且根據預設不再顯示於 Visual Studio 工具箱中。 您可以手動將控制項新增至工具箱。

1. 依上述指示安裝 WinForms 或 WebForms 的 Nuget 套件。

2. 移除工具箱中所列出的報表檢視器控制項。

    ![ssRS-remove-old-rvcontrol-toolbox](../../reporting-services/application-integration/media/ssrs-remove-old-rvcontrol-toolbox.png)

3. 以滑鼠右鍵按一下工具箱的任何位置，然後選取 [選擇項目...]。

    ![ssRS-toolbox-choose-item](../../reporting-services/application-integration/media/ssrs-toolbox-choose-item.png)
    
4. 在 [.NET Framework 元件] 中選取 [瀏覽]。

    ![ssRS-toolbox-browse](../../reporting-services/application-integration/media/ssrs-toolbox-browse.png)

5. 從安裝的 Nuget 套件中選取 **Microsoft.ReportViewer.WinForms.dll** 或 **Microsoft.ReportViewer.WebForms.dll**。

    > [!NOTE] 
    > Nuget 套件會安裝在專案的解決方案目錄中。 dll 的路徑類似：`{Solution Directory}\packages\Microsoft.ReportingServices.ReportViewerControl.Winforms.{version}\lib\net40` 或 `{Solution Directory}\packages\Microsoft.ReportingServices.ReportViewerControl.WebForms.{version}\lib\net40`。

6. 新的控制項應該顯示在 [工具箱] 中。 如希望，您可以將它移動至工具箱的另一個索引標籤中。

    ![ssRS-toolbox-rvcontrol](../../reporting-services/application-integration/media/ssrs-toolbox-rvcontrol.png)

## <a name="common-issues"></a>常見的問題
    
檢視器控制項是為現代瀏覽器所設計。 如果瀏覽器使用 IE 相容性模式呈現頁面，則控制項可能無法正常運作。 內部網路網站可能需要中繼標籤覆寫預設瀏覽器行為。

    ```
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    ```
      
## <a name="feedback"></a>意見反應

讓小組了解 [Reporting Services 論壇](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=sqlreportingservices)上的問題。

## <a name="see-also"></a>另請參閱

[報表檢視器控制項中的資料收集](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls-data-collection.md)  
更多問題嗎？ [試試 Reporting Services 論壇](https://go.microsoft.com/fwlink/?LinkId=620231)

