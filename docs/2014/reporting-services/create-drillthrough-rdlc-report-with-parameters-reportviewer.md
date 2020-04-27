---
title: 使用 ReportViewer 建立具有參數的鑽取（.RDLC）報表（SSRS 教學課程） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 628c8775-c62d-45ac-b349-23db86fa4e6c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7efb713b5dbf9a3f19118bb3572ccd35778aad19
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66109653"
---
# <a name="create-a-drillthrough-rdlc-report-with-parameters-using-reportviewer-ssrs-tutorial"></a>使用 ReportViewer 建立包含參數的鑽研 (RDLC) 報表 (SSRS 教學課程)
  [鑽研](https://technet.microsoft.com/library/ff519554.aspx) 報表是使用者從另一個報表按一下連結所開啟的報表。 鑽研報表通常包含有關原始摘要報表之項目的詳細資料。 本教學課程將逐步引導您進行下列課程，以[本機模式報表](local-vs-connected-mode-report-viewer-reporting-services-sharepoint-mode.md)建立包含參數和查詢的鑽研報表。  
  
## <a name="requirements"></a>需求  
 若要使用此逐步解說，您必須具有**AdventureWorks2008**範例資料庫的存取權。 本逐步解說中使用的查詢也會使用**AdventureWorks2012**資料庫。 如需如何取得**AdventureWorks2008**範例資料庫的詳細資訊，請參閱逐步解說：安裝適用于 Microsoft Visual Studio 2010[的 AdventureWorks 資料庫](https://msdn.microsoft.com/library/aa992075\(v=vs.100\).aspx)。  
  
 本逐步解說假設您熟悉 Transaction-SQL 查詢以及 ADO.NET [DataSet](https://msdn.microsoft.com/library/system.data.dataset\(v=vs.100\).aspx) 和 [DataTable](https://msdn.microsoft.com/library/system.data.datatable\(v=vs.100\).aspx) 物件。  
  
 使用 Visual Studio 2010 或 Visual Studio 2012 和 ASP.NET 網站範本建立包含 ReportViewer 控制項的 ASP.NET 網頁。 控制項會設定為檢視您所建立的報表。 在此逐步解說中，您會使用 Microsoft Visual C# 建立應用程式。  
  
## <a name="tasks"></a>工作  
 [第1課：建立新的網站](../reporting-services/lesson-1-create-a-new-web-site.md)   
 [第2課：定義父報表的資料連線和資料表](../reporting-services/lesson-2-define-a-data-connection-and-data-table-for-parent-report.md)   
 [第3課：使用報表精靈設計父報表](../reporting-services/lesson-3-design-the-parent-report-using-the-report-wizard.md)   
 [第4課：定義子報表的資料連線和資料表](../reporting-services/lesson-4-define-a-data-connection-and-data-table-for-child-report.md)   
 [第5課：使用報表精靈設計子報表](../reporting-services/lesson-5-design-the-child-report-using-the-report-wizard.md)   
 [第6課：將 ReportViewer 控制項加入至應用程式](../reporting-services/lesson-6-add-a-reportviewer-control-to-the-application.md)   
 [第7課：在父報表上加入鑽取動作](../reporting-services/lesson-7-add-drillthrough-action-on-parent-report.md)   
 [第8課：建立資料篩選](../reporting-services/lesson-8-create-a-data-filter.md)   
 [第 9 課：建置及執行應用程式](../reporting-services/lesson-9-build-and-run-the-application.md)  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services SSRS &#40;的教學課程&#41;](../reporting-services/reporting-services-tutorials-ssrs.md)   
 [使用報表設計師設計報表 &#40;SSRS&#41;](tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md)  
  
  
