---
title: "第 6 課： 將 ReportViewer 控制項加入至應用程式 |Microsoft 文件"
ms.custom: 
ms.date: 05/18/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: f9492a97-5609-4059-ae76-0fba111d4968
caps.latest.revision: 7
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 914d8abf2ad7b72b5ce1035da2867c47b67dfa14
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="lesson-6-add-a-reportviewer-control-to-the-application"></a>第 6 課：將 ReportViewer 控制項加入到應用程式
使用 [報表精靈] 設計子報表之後，下一步是要將 ReportViewer 控制項加入至網站應用程式。 如果您是使用 ASP.NET 報表網站，它會將 ReportViewer 控制項新增至 default.aspx 頁面。   
  
### <a name="to-add-a-reportviewer-control-to-the-application"></a>若要將 ReportViewer 控制項加入至應用程式  
  
1.  在**方案總管**中，以滑鼠右鍵按一下 **Default.aspx**，再按一下 [檢視表設計工具]。  
  
2.  如果 default.aspx 中已具備 ReportViewer 控制項，請跳至**步驟 4**。 從 [工具箱] 視窗的 [AJAX 擴充功能] 群組中，將 **ScriptManager** 控制項拖曳至設計介面。  
  
3.  從 [報表] 群組，將 **ReportViewer** 控制項拖曳至設計介面上的 **ScriptManager** 控制項下方。  
  
4.  按一下 **ReportViewer** 控制項右上角的箭頭，開啟 [ReportViewer 工作] 視窗。  
  
5.  在 [選擇報表] 方塊中，選取您建立的父報表。  
  
    當您選取報表時，報表中所使用的資料來源執行個體會自動建立。 產生的程式碼會具現化每個 DataTable (及其 [DataSet](http://msdn.microsoft.com/library/system.data.dataset.aspx) 容器)。 [ObjectDataSource](http://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.aspx) 控制項會新增至設計介面，對應報表中使用的每個資料來源。 此資料來源控制項會自動設定。  
  
6.  在 [建置] 功能表上，按一下 [建置網站]。  
  
    報表會進行編譯，而報表運算式中的任何錯誤 (像是語法錯誤) 都會出現在 [錯誤清單] 區域中。 按一下 Visual Studio 視窗底部的 [錯誤清單]，顯示 [錯誤清單] 區域。  
  
## <a name="next-task"></a>下一項工作  
您已成功將 ReportViewer 控制項加入至網站應用程式。 接下來您將在父報表上加入鑽研動作。 請參閱 [第 7 課：在父報表上加入鑽研動作](../reporting-services/lesson-7-add-drillthrough-action-on-parent-report.md)。  
  


