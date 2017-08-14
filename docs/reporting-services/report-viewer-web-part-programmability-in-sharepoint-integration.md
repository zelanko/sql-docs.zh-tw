---
title: "報表檢視器 Web 組件可程式性在 SharePoint 整合 |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
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
ms.assetid: 714017b7-1bd6-4950-a3c6-d0df8450a877
caps.latest.revision: 8
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 9339b0f383efd757e9be49271f4a5bdd2d7a4d4f
ms.contentlocale: zh-tw
ms.lasthandoff: 08/12/2017

---
# <a name="report-viewer-web-part-programmability-in-sharepoint-integration"></a>SharePoint 整合中的報表檢視器 Web 組件可程式性
  報表檢視器 Web 組件是伺服器控制項，其中包含一組公用應用程式開發介面 (API)，可讓開發人員建立自訂 SharePoint 應用程式。 您可以建立自訂 Web 組件，利用 Web 組件連接提供報表路徑和參數給報表檢視器 Web 組件。 您也可以將 Web 組件內嵌在自訂 SharePoint Web 組件頁面中，並使用公用 API 來自訂該組件。  
  
## <a name="connecting-to-report-viewer-web-part-with-custom-web-parts"></a>使用自訂 Web 組件連接到報表檢視器 Web 組件  
 報表檢視器 Web 組件是 SharePoint Web 組件實作的連接取用者<xref:System.Web.UI.WebControls.WebParts.IWebPartRow>或 T:Microsoft.SharePoint.WebPartPages.IFilterValues。 <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> Web 組件，例如**文件**Web 組件可以提供報表路徑給報表檢視器 Web 組件放在相同的 Web 組件頁面上，為報表檢視器 Web 組件時。 同樣地，T:Microsoft.SharePoint.WebPartPages.IFilterValues Web 組件，例如**文字篩選**或**選擇篩選**，可以提供報表參數給報表檢視器 Web 組件放在相同的 Web 組件頁面上，為報表檢視器 Web 組件時。  
  
### <a name="implementing-a-report-path-provider-with-iwebpartrow"></a>使用 IWebPartRow 實作報表路徑提供者  
 若要透過 Web 組件連接將報表路徑提供給報表檢視器 Web 組件，請執行以下作業：  
  
1.  建立實作 <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> 介面的 Web 組件。  
  
2.  將此 Web 組件加入至與報表檢視器 Web 組件相同的 Web 組件頁面上。  
  
3.  在 Web 式 Web 組件設計使用者介面上，將您的 Web 組件連接到報表檢視器 Web 組件。  
  
    > [!NOTE]  
    >  您可以只連接一個<xref:System.Web.UI.WebControls.WebParts.IWebPartRow>網頁組件以報表檢視器 Web 組件，在一段期間，而且您無法連接兩者<xref:System.Web.UI.WebControls.WebParts.IWebPartRow>Web 組件和報表檢視器 Web 組件，同時 T:Microsoft.SharePoint.WebPartPages.IFilterValues 網頁組件。  
  
 針對您<xref:System.Web.UI.WebControls.WebParts.IWebPartRow>Web 組件，才能正常使用 t: microsoft.reportingservices.sharepoint.ui.webparts.reportviewerwebpart<，您必須執行下列<xref:System.Web.UI.WebControls.WebParts.IWebPartRow.GetRowData%2A>方法：  
  
-   使用 <xref:System.Data.DataRowView> 物件當做輸入參數來叫用回撥方法。  
  
-   確定 <xref:System.Data.DataRowView> 物件包含名為 "DocUrl" 的資料行 (其中包含報表路徑)。  
  
    > [!NOTE]  
    >  適用於 [!INCLUDE[offSPServ](../includes/offspserv-md.md)] 2010 的報表檢視器 Web 組件也支援使用 "FileRef" 資料行接收報表路徑。  
  
### <a name="implementing-a-report-parameter-provider-with-ifiltervalues"></a>使用 IFilterValues 實作報表參數提供者  
 Web 組件可實作 T:Microsoft.SharePoint.WebPartPages.IFilterValues 可以提供一個參數值給報表檢視器 Web 組件。 傳送給報表檢視器 Web 組件的參數值會受到與報表參數相同的限制，如同報表定義中所指定 (例如資料類型、有效值等等)。  
  
 若要將報表參數提供給報表檢視器 Web 組件，請執行以下作業：  
  
1.  建立 Web 組件可實作 T:Microsoft.SharePoint.WebPartPages.IFilterValues 介面。  
  
2.  將 Web 組件加入至 t: microsoft.reportingservices.sharepoint.ui.webparts.reportviewerwebpart< 同一個頁面。  
  
3.  您 T:Microsoft.SharePoint.WebPartPages.IFilterValues Web 組件連接到報表檢視器 Web 組件在 Web 式 Web 組件設計使用者介面。  
  
    > [!NOTE]  
    >  您可以連接到報表檢視器 Web 組件的多個 T:Microsoft.SharePoint.WebPartPages.IFilterValues Web 組件，一次。 不過，您無法連接兩者<xref:System.Web.UI.WebControls.WebParts.IWebPartRow>Web 組件和報表檢視器 Web 組件，同時 T:Microsoft.SharePoint.WebPartPages.IFilterValues 網頁組件。  
  
  
