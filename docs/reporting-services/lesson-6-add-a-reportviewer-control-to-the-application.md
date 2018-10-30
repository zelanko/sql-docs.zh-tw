---
title: 第 6 課：將 ReportViewer 控制項新增至應用程式 | Microsoft Docs
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: f9492a97-5609-4059-ae76-0fba111d4968
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ba16d32c5a44385329f789c2e0851609514be616
ms.sourcegitcommit: 3daacc4198918d33179f595ba7cd4ccb2a13b3c0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/25/2018
ms.locfileid: "50028567"
---
# <a name="lesson-6-add-a-reportviewer-control-to-the-application"></a>第 6 課：將 ReportViewer 控制項加入到應用程式
使用 [報表精靈] 設計子報表之後，下一步是要將 ReportViewer 控制項加入至網站應用程式。 如果您是使用 ASP.NET 報表網站，它會將 ReportViewer 控制項新增至 default.aspx 頁面。   
  
### <a name="to-add-a-reportviewer-control-to-the-application"></a>若要將 ReportViewer 控制項加入至應用程式  
  
1.  在**方案總管**中，以滑鼠右鍵按一下 **Default.aspx**，然後按一下 [檢視表設計師]。  
  
2.  如果 default.aspx 中已具備 ReportViewer 控制項，請跳至 **步驟 4**。 從 [工具箱] 視窗的 [AJAX 延伸模組] 群組中，將 **ScriptManager** 控制項拖曳至設計介面。  
  
3.  從 [報表] 群組，將 **ReportViewer** 控制項拖曳至設計介面上的 **ScriptManager** 控制項下方。  
  
4.  按一下 **ReportViewer** 控制項右上角的箭頭，開啟 [ReportViewer 工作] 視窗。  
  
5.  在 [選擇報表] 方塊中，選取您建立的父報表。  
  
    當您選取報表時，報表中所使用的資料來源執行個體會自動建立。 產生的程式碼會具現化每個 DataTable (及其 [DataSet](https://msdn.microsoft.com/library/system.data.dataset.aspx) 容器)。 [ObjectDataSource](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.aspx) 控制項會新增至設計介面，對應報表中使用的每個資料來源。 此資料來源控制項會自動設定。  
  
6.  在 [建置] 功能表上，按一下 [建置網站]。  
  
    報表會進行編譯，而報表運算式中的任何錯誤 (像是語法錯誤) 都會出現在 [錯誤清單] 區域中。 按一下 Visual Studio 視窗底部的 [錯誤清單]，顯示 [錯誤清單] 區域。  
  
## <a name="next-task"></a>下一項工作  
您已成功將 ReportViewer 控制項加入至網站應用程式。 接下來您將在父報表上加入鑽研動作。 請參閱 [第 7 課：在父報表上加入鑽研動作](../reporting-services/lesson-7-add-drillthrough-action-on-parent-report.md)。  
  

