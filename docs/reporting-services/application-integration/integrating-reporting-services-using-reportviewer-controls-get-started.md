---
title: "開始使用 ReportViewer 2016 控制項 |Microsoft 文件"
ms.custom: 
ms.date: 06/12/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 01a821c4-2920-400c-be03-93d26c749bb1
caps.latest.revision: 12
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: a6a0bbee9141df565966df3e90f396e33c9b96a7
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="integrating-reporting-services-using-reportviewer-controls---get-started"></a>整合 Reporting Services 使用 ReportViewer 控制項-快速入門

了解如何開發人員可以在 ASP.Net 網站和 Windows forms 應用程式，透過 Reporting Services 2016 ReportViewer 控制項內嵌分頁的報表。 您可以將控制項加入新的專案，或更新現有的專案。

## <a name="adding-the-reportviewer-control-to-a-new-web-project"></a>將 ReportViewer 控制項加入至新的 web 專案

1. 建立新**ASP.NET 空網站**或開啟現有的 ASP.NET 專案。

    ![ssRS 建立--專案間的新 ASPNET](../../reporting-services/application-integration/media/ssrs-create-new-aspnet-project.png)

2. 安裝 ReportViewer 2016 控制項 nuget 封裝，透過**Nuget 封裝管理員主控台**。

    ```
    Install-Package Microsoft.ReportingServices.ReportViewerControl.WebForms
    ```
3. 專案中加入新的.aspx 網頁，並註冊頁面中使用 ReportViewer 控制項組件。

    ```
    <%@ Register assembly="Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" namespace="Microsoft.Reporting.WebForms" tagprefix="rsweb" %>
    ```
    
4. 新增**ScriptManagerControl**至頁面。

5. 將 ReportViewer 控制項加入至頁面。 以下程式碼片段可以更新為參考的遠端報表伺服器上裝載的報表。

    ```
    <rsweb:ReportViewer ID="ReportViewer1" runat="server" ProcessingMode="Remote">
      <ServerReport ReportPath="" ReportServerUrl="" />
    </rsweb:ReportViewer>
    ```
    
最後一頁看起來應該如下所示。

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

要使用現有的專案中 ReportViewer 2016 控制項、 將透過 Nuget 控制項加入和更新版本的組件參考*版本為 14.0.0.0*。 這包括正在更新專案的 web.config 和所有參考的 ReportViewer 控制項的.aspx 網頁。

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

### <a name="sample-aspx"></a>範例.aspx

```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs" Inherits="SampleAspx" %>

<!-- Update version to 14.0.0.0 -->
<%@ Register assembly="Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" namespace="Microsoft.Reporting.WebForms" tagprefix="rsweb" %>

<!DOCTYPE html>
```

## <a name="adding-the-reportviewer-control-to-a-new-windows-forms-project"></a>將 ReportViewer 控制項加入至新的 Windows form 專案

1. 建立新**Windows Forms 應用程式**或開啟現有的專案。

    ![ssRS 建立--專案間的新 winforms](../../reporting-services/application-integration/media/ssrs-create-new-winforms-project.png)

2. 安裝 ReportViewer 2016 控制項 nuget 封裝，透過**Nuget 封裝管理員主控台**。

    ```
    Install-Package Microsoft.ReportingServices.ReportViewerControl.WinForms
    ```
3. 從程式碼中加入新控制項或[將控制項加入 [工具箱]](##adding-control-to-visual-studio-toolbar)。

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

## <a name="how-to-set-100-height-on-the-report-viewer-2016-control"></a>如何設定報表檢視器 2016年控制項上的 100%的高度

新的報表檢視器 2016年控制項最適合用於 HTML5 標準模式的頁面，適用於所有現代化瀏覽器。 在過去，與舊 RVC 控制項，當您設定 100 %height 屬性，它即使沒有任何上階必須指定高度。 此行為已經變更 html5 格式。 當您在新的 RVC 控制項上設定此屬性時，則在父項目已定義的高度時，才會正確運作，也就是不是自動的值或所有上階的 RVC 也有 100%的高度。

以下是兩個範例，若要這樣做。

### <a name="by-setting-the-height-of-all-the-parent-elements-to-100"></a>將所有父系的高度項目設定為 100%

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

### <a name="by-setting-the-style-height-attribute-on-the-parent-of-the-reportviewer-control"></a>藉由設定 reportviewer 控制項的父代上的樣式高度屬性

如需檢視區百分比長度的詳細資訊，請參閱[檢視區百分比長度](https://www.w3.org/TR/css3-values/#viewport-relative-lengths)。

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

## <a name="adding-control-to-visual-studio-toolbar"></a>將控制項加入至 Visual Studio 工具列

報表檢視器控制項現在隨附以 NuGet 套件。 因為這個緣故，不會看到顯示 Visual Studio 工具箱中的預設報表檢視器控制項。 您可以將控制項加入工具箱 中，執行下列動作。

1. WinForms 或 WebForms 如上面所述安裝 NuGet 套件。

2. 在工具箱中移除所列的 ReportViewer 控制項。 這是 12.x 的版本控制。

    ![ssRS-移除-舊-rvcontrol-工具箱](../../reporting-services/application-integration/media/ssrs-remove-old-rvcontrol-toolbox.png)

3. 以滑鼠右鍵按一下在任何位置工具箱 中，然後選取**選擇項目...**.

    ![ssRS 工具箱-選擇的項目](../../reporting-services/application-integration/media/ssrs-toolbox-choose-item.png)
    
4. 在**.NET Framework 元件**，選取**瀏覽**。

    ![瀏覽工具箱 ssRS](../../reporting-services/application-integration/media/ssrs-toolbox-browse.png)

5. 選取**Microsoft.ReportViewer.WinForms.dll**或**Microsoft.ReportViewer.WebForms.dll**從您安裝 NuGet 封裝。

    > [!NOTE] 
    > 您的專案的方案目錄中，將會安裝 NuGet 封裝。 Dll 的路徑必須與下列類似：`{Solution Directory}\packages\Microsoft.ReportingServices.ReportViewerControl.Winforms.{version}\lib\net40`或`{Solution Directory}\packages\Microsoft.ReportingServices.ReportViewerControl.WebForms.{version}\lib\net40`。

6. 新的控制項應該顯示在 [工具箱] 中。 您可以將其移動至另一個索引標籤，工具箱內視。

    ![ssRS-工具箱-rvcontrol](../../reporting-services/application-integration/media/ssrs-toolbox-rvcontrol.png)

### <a name="things-to-be-aware-of"></a>要注意的事項

- 這會新增在目前專案中安裝的 NuGet 套件的參考。 [工具箱] 中的項目會保存至其他專案。 當您安裝 NuGet 封裝在新的方案/專案中時，工具箱項目也可能會參照較舊的版本。 

- 即使組件不再可用時，控制項仍在 [工具箱]。 若已刪除該專案，Visual Studio 將會擲回錯誤如果再次嘗試將控制項從 [工具箱]。 若要更正這個錯誤，從 [工具箱] 移除控制項並重新加入使用上述步驟。


## <a name="common-issues"></a>常見的問題
    
- ReportViewer 2016 控制項被為了搭配新式瀏覽器。 如果瀏覽器中呈現網頁 IE 相容性模式中，控制項可能無法運作。 內部網路網站可能需要其中鼓勵轉譯相容性模式中的內部網路頁面 meta 標記，來覆寫設定。

    ```
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    ```
      
## <a name="providing-feedback"></a>提供意見反應

可讓小組了解您的控制項會遇到的問題[Reporting Services MSDN 論壇](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=sqlreportingservices)或透過電子郵件在[ RVCFeedback@microsoft.com ](mailto:RVCFeedback@microsoft.com)。

## <a name="see-also"></a>另請參閱

[2016 ReportingViewer 控制項中的資料收集](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls-data-collection.md)  
更多問題嗎？ [再試一次 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)


