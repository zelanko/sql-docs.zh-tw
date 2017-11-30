---
title: "第 5 課：使用報表精靈設計子報表 | Microsoft Docs"
ms.custom: 
ms.date: 05/18/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: 19a3f927-ea97-4f40-a5f8-cd5f2598e4da
caps.latest.revision: "8"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: b84722749ad94251c057a43858e2da98b37d2adb
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="lesson-5-design-the-child-report-using-the-report-wizard"></a>第 5 課：使用報表精靈設計子報表
在您建立子報表的資料連接和資料表之後，下一步是要使用報表設計師中的 [報表精靈] 設計子報表。 如需報表設計師的詳細資訊，請參閱[使用報表設計師設計報表 &#40;SSRS&#41;](../reporting-services/tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md)。  
  
### <a name="to-design-the-child-report-using-the-report-wizard"></a>若要使用報表精靈設計子報表  
  
1.  請確認已在 **方案總管**中選取頂層網站。  
  
2.  以滑鼠右鍵按一下網站，然後選取 [新增項目]。  
  
3.  在 [新增項目] 對話方塊中，按一下 [報表精靈]，輸入報表檔案的名稱，然後選取 [新增]。  
  
    這樣會啟動 [報表精靈]。  
  
4.  在 [資料集屬性] 頁面的 [資料來源] 中，選取 **DataSet2**。  
  
    [可用資料集] 方塊會自動更新為您所建立的 DataTable。  
  
5.  選取 **[下一步]**。  
  
6.  在 [排列欄位] 頁面中執行下列操作：  
  
    1.  將 **ProductID**、**PurchaseOrderID**、**PurchaseOrderDetailID**、**OrderQty**、**ReceivedQty**、**RejectedQty** 和 **StockedQty** 從 [可用欄位] 拖曳至 [值] 方塊。  
  
    2.  按一下 **Sum(ProductID)**、**Sum(PurchaseOrderID)**、**Sum(PurchaseOrderDetailID)**、**Sum(OrderQty)**、**Sum(ReceivedQty)**、**Sum(RejectedQty)** 和 **Sum(StockedQty)** 旁的箭頭，並清除 [Sum] 選項。  
  
7.  連選兩次 [下一步]，然後選取 [完成] 關閉 [報表精靈]。  
  
    現在您已建立 .rdlc 檔。 此檔案會在報表設計師中開啟。 您設計的 Tablix 現在會顯示於設計介面中。  
  
8.  在 .rdlc 檔開啟的情況下，執行下列操作加入參數：  
  
    1.  以滑鼠右鍵按一下 [報表資料] 窗格中的 [參數]，然後選取 [新增參數]。  
  
    2.  在 [名稱] 方塊中，輸入 **productid**。  
  
    3.  確認已在 [資料類型] 清單方塊中，選取 [整數]。  
  
    4.  按一下 **[確定]**。  
  
9. 儲存 .rdlc 檔。  
  
## <a name="next-task"></a>下一項工作  
您已使用 [報表精靈] 成功設計子報表。 接下來您要將 ReportViewer 控制項加入至網站應用程式。 請參閱 [第 6 課：將 ReportViewer 控制項加入至應用程式](../reporting-services/lesson-6-add-a-reportviewer-control-to-the-application.md)。  
  
  
  

