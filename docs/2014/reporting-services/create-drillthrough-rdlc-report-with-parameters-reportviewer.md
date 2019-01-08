---
title: 建立使用 ReportViewer （SSRS 教學課程） 參數的鑽研 (RDLC) 報表 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 628c8775-c62d-45ac-b349-23db86fa4e6c
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: f04a797540abdde31411978ca05b776ee7693bd5
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53352077"
---
# <a name="create-a-drillthrough-rdlc-report-with-parameters-using-reportviewer-ssrs-tutorial"></a>使用 ReportViewer 建立包含參數的鑽研 (RDLC) 報表 (SSRS 教學課程)
  [鑽研](https://technet.microsoft.com/library/ff519554.aspx)報表是使用者從另一個報表按一下連結所開啟的報表。 鑽研報表通常包含有關原始摘要報表之項目的詳細資料。 本教學課程將逐步引導您進行下列課程，以 [本機模式報表](local-vs-connected-mode-report-viewer-reporting-services-sharepoint-mode.md)建立包含參數和查詢的鑽研報表。  
  
## <a name="requirements"></a>需求  
 若要使用本逐步解說中，您必須具有存取權**AdventureWorks2008**範例資料庫。 本逐步解說中使用的查詢也可搭配**AdventureWorks2012**資料庫。 如需有關如何取得**AdventureWorks2008**範例資料庫，請參閱[逐步解說：安裝 AdventureWorks 資料庫](https://msdn.microsoft.com/library/aa992075\(v=vs.100\).aspx)for Microsoft Visual Studio 2010。  
  
 本逐步解說假設您熟悉 Transaction-SQL 查詢以及 ADO.NET [DataSet](https://msdn.microsoft.com/library/system.data.dataset\(v=vs.100\).aspx) 和 [DataTable](https://msdn.microsoft.com/library/system.data.datatable\(v=vs.100\).aspx) 物件。  
  
 使用 Visual Studio 2010 或 Visual Studio 2012 和 ASP.NET 網站範本建立包含 ReportViewer 控制項的 ASP.NET 網頁。 控制項會設定為檢視您所建立的報表。 在此逐步解說中，您會使用 Microsoft Visual C# 建立應用程式。  
  
## <a name="tasks"></a>工作  
 [第 1 課：建立新的網站](../reporting-services/lesson-1-create-a-new-web-site.md)   
 [第 2 課：定義父報表的資料連接和資料表](../reporting-services/lesson-2-define-a-data-connection-and-data-table-for-parent-report.md)   
 [第 3 課：設計父報表使用報表精靈](../reporting-services/lesson-3-design-the-parent-report-using-the-report-wizard.md)   
 [第 4 課：定義子報表的資料連接和資料表](../reporting-services/lesson-4-define-a-data-connection-and-data-table-for-child-report.md)   
 [第 5 課：設計子報表使用報表精靈](../reporting-services/lesson-5-design-the-child-report-using-the-report-wizard.md)   
 [第 6 課：將 ReportViewer 控制項新增至應用程式](../reporting-services/lesson-6-add-a-reportviewer-control-to-the-application.md)   
 [第 7 課：在父報表上加入鑽研動作](../reporting-services/lesson-7-add-drillthrough-action-on-parent-report.md)   
 [第 8 課：建立資料篩選](../reporting-services/lesson-8-create-a-data-filter.md)   
 [第 9 課：建置並執行應用程式](../reporting-services/lesson-9-build-and-run-the-application.md)  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 教學課程 &#40;SSRS&#41;](../reporting-services/reporting-services-tutorials-ssrs.md)   
 [使用報表設計師設計報表 &#40;SSRS&#41;](tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md)  
  
  
