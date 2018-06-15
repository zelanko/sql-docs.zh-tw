---
title: 建立具有參數的鑽研 (RDLC) 報表 - ReportViewer | Microsoft Docs
ms.custom: ''
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: reporting-services
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: 628c8775-c62d-45ac-b349-23db86fa4e6c
caps.latest.revision: 8
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: f90ac792fe849ca91735e5a9b22a399d7798cf23
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33014595"
---
# <a name="create-drillthrough-rdlc-report-with-parameters---reportviewer"></a>建立具有參數的鑽研 (RDLC) 報表 - ReportViewer
[鑽研](http://technet.microsoft.com/library/ff519554.aspx) 報表是使用者從另一個報表按一下連結所開啟的報表。 鑽研報表通常包含有關原始摘要報表之項目的詳細資料。 本教學課程將逐步引導您進行下列課程，以 [本機模式報表](http://msdn.microsoft.com/library/ff487969.aspx)建立包含參數和查詢的鑽研報表。  
  
## <a name="requirements"></a>需求  
若要使用此逐步解說，您必須能夠存取 **AdventureWorks2014** 範例資料庫。 如需如何取得 **AdventureWorks2014** 範例資料庫的詳細資訊，請參閱 [AdventureWorks 範例資料庫](https://github.com/Microsoft/sql-server-samples/releases)。  
  
本逐步解說假設您熟悉 Transaction-SQL 查詢以及 ADO.NET [DataSet](https://msdn.microsoft.com/library/system.data.dataset.aspx) 和 [DataTable](http://msdn.microsoft.com/library/system.data.datatable.aspx) 物件。  
  
使用 Visual Studio 2015 和 ASP.NET Web 應用程式，建立包含 ReportViewer 控制項的 ASP.NET 網頁。 控制項會設定為檢視您所建立的報表。 在此逐步解說中，您會使用 Microsoft Visual C# 建立應用程式。  
  
## <a name="tasks"></a>工作  
[第 1 課：建立新的網站](../reporting-services/lesson-1-create-a-new-web-site.md)  
[第 2 課：定義父報表的資料連線和資料表](../reporting-services/lesson-2-define-a-data-connection-and-data-table-for-parent-report.md)  
[第 3 課：使用報表精靈設計父報表](../reporting-services/lesson-3-design-the-parent-report-using-the-report-wizard.md)  
[第 4 課：定義子報表的資料連線和資料表](../reporting-services/lesson-4-define-a-data-connection-and-data-table-for-child-report.md)  
[第 5 課：使用報表精靈設計子報表](../reporting-services/lesson-5-design-the-child-report-using-the-report-wizard.md)  
[第 6 課：將 ReportViewer 控制項加入到應用程式](../reporting-services/lesson-6-add-a-reportviewer-control-to-the-application.md)  
[第 7 課：在父報表上加入鑽研動作](../reporting-services/lesson-7-add-drillthrough-action-on-parent-report.md)  
[第 8 課：建立資料篩選](../reporting-services/lesson-8-create-a-data-filter.md)  
[Lesson 9: Build and Run the Application](../reporting-services/lesson-9-build-and-run-the-application.md)  
  
## <a name="see-also"></a>另請參閱  
[Reporting Services 教學課程 &#40;SSRS&#41;](../reporting-services/reporting-services-tutorials-ssrs.md)  
[使用報表設計師設計報表 &#40;SSRS&#41;](../reporting-services/tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md)  
  

