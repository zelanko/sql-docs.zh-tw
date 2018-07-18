---
title: SharePoint 整合中的報表檢視器網頁組件可程式性 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: reporting-services
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 714017b7-1bd6-4950-a3c6-d0df8450a877
caps.latest.revision: 8
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 7a953b61175d6790c5d0504e0e6bbb74ccfc2d9f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33026109"
---
# <a name="report-viewer-web-part-programmability-in-sharepoint-integration"></a>SharePoint 整合中的報表檢視器 Web 組件可程式性
  報表檢視器網頁組件是伺服器控制項，這個控制項包含一組公用應用程式開發介面 (API)，可讓開發人員建立自訂 SharePoint 應用程式。 您可以建立自訂 Web 組件，利用 Web 組件連接提供報表路徑和參數給報表檢視器 Web 組件。 您也可以將 Web 組件內嵌在自訂 SharePoint Web 組件頁面中，並使用公用 API 來自訂該組件。  
  
## <a name="connecting-to-report-viewer-web-part-with-custom-web-parts"></a>使用自訂 Web 組件連接到報表檢視器 Web 組件  
 報表檢視器網頁組件是實作 <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> 或 T:Microsoft.SharePoint.WebPartPages.IFilterValues 之 SharePoint 網頁組件的連線取用者。 如果將 <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> 網頁組件 (例如**文件**網頁組件) 放在與報表檢視器網頁組件相同的網頁組件頁面上，此網頁組件也可以提供報表路徑給報表檢視器網頁組件。 同樣地，如果將 T:Microsoft.SharePoint.WebPartPages.IFilterValues 網頁組件 (例如**文字篩選**或**選擇篩選**) 放在與報表檢視器網頁組件相同的網頁組件頁面上，此網頁組件也可以提供報表參數給報表檢視器網頁組件。  
  
### <a name="implementing-a-report-path-provider-with-iwebpartrow"></a>使用 IWebPartRow 實作報表路徑提供者  
 若要透過 Web 組件連接將報表路徑提供給報表檢視器 Web 組件，請執行以下作業：  
  
1.  建立實作 <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> 介面的 Web 組件。  
  
2.  將此 Web 組件加入至與報表檢視器 Web 組件相同的 Web 組件頁面上。  
  
3.  在 Web 式 Web 組件設計使用者介面上，將您的 Web 組件連接到報表檢視器 Web 組件。  
  
    > [!NOTE]  
    >  您一次只能將一個 <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> 網頁組件連線到報表檢視器網頁組件，不能同時將 <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> 網頁組件和 T:Microsoft.SharePoint.WebPartPages.IFilterValues 網頁組件連線到報表檢視器網頁組件。  
  
 為使您的 <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> 網頁組件與 T:Microsoft.ReportingServices.SharePoint.UI.WebParts.ReportViewerWebPart一起正常運作，您必須在 <xref:System.Web.UI.WebControls.WebParts.IWebPartRow.GetRowData%2A> 方法中執行下列作業：  
  
-   使用 <xref:System.Data.DataRowView> 物件當做輸入參數來叫用回撥方法。  
  
-   確定 <xref:System.Data.DataRowView> 物件包含名為 "DocUrl" 的資料行 (其中包含報表路徑)。  
  
    > [!NOTE]  
    >  適用於 [!INCLUDE[offSPServ](../includes/offspserv-md.md)] 2010 的報表檢視器 Web 組件也支援使用 "FileRef" 資料行接收報表路徑。  
  
### <a name="implementing-a-report-parameter-provider-with-ifiltervalues"></a>使用 IFilterValues 實作報表參數提供者  
 實作 T:Microsoft.SharePoint.WebPartPages.IFilterValues 的網頁組件可以提供一個參數值給報表檢視器網頁組件。 傳送給報表檢視器 Web 組件的參數值會受到與報表參數相同的限制，如同報表定義中所指定 (例如資料類型、有效值等等)。  
  
 若要將報表參數提供給報表檢視器 Web 組件，請執行以下作業：  
  
1.  建立實作 T:Microsoft.SharePoint.WebPartPages.IFilterValues 介面的網頁組件。  
  
2.  將網頁組件新增至與 T:Microsoft.ReportingServices.SharePoint.UI.WebParts.ReportViewerWebPart 相同的頁面。  
  
3.  在網頁式網頁組件設計使用者介面中，將您的 T:Microsoft.SharePoint.WebPartPages.IFilterValues 網頁組件連線到報表檢視器網頁組件。  
  
    > [!NOTE]  
    >  您可以一次將多個 T:Microsoft.SharePoint.WebPartPages.IFilterValues 網頁組件連線到報表檢視器網頁組件。 但是不能同時將 <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> 網頁組件和 T:Microsoft.SharePoint.WebPartPages.IFilterValues 網頁組件連線到報表檢視器網頁組件。  
  
  
