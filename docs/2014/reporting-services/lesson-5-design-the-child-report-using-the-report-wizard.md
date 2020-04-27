---
title: 第 5 課：使用報表精靈設計子報表 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 19a3f927-ea97-4f40-a5f8-cd5f2598e4da
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 661b4f3cc63eb0c19fddb53f872e940d1f9976e2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66108443"
---
# <a name="lesson-5-design-the-child-report-using-the-report-wizard"></a>第 5 課：使用報表精靈設計子報表
  在您建立子報表的資料連接和資料表之後，下一步是要使用報表設計師中的 [報表精靈] 設計子報表。 如需報表設計師的詳細資訊，請參閱[使用報表設計師設計報表 &#40;SSRS&#41;](tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md)。  
  
### <a name="to-design-the-child-report-using-the-report-wizard"></a>若要使用報表精靈設計子報表  
  
1.  請確認已在 **方案總管**中選取頂層網站。  
  
2.  以滑鼠右鍵按一下網站，然後選取 [新增項目]  。  
  
3.  在 [**加入新專案**] 對話方塊中，按一下 [**報表 Wizard]**，輸入報表檔案的名稱，然後按一下 [**新增**]。  
  
     這樣會啟動 [報表精靈]。  
  
4.  在 [資料**集屬性**] 頁面的 [**資料來源**] 方塊中，按一下 [ **DataSet2**]。  
  
     [可用資料集]  方塊會自動更新為您所建立的 DataTable。  
  
5.  按 [下一步]  。  
  
6.  在 [排列欄位]  頁面中執行下列操作：  
  
    1.  將 **ProductID**、**PurchaseOrderID**、**PurchaseOrderDetailID**、**OrderQty**、**ReceivedQty**、**RejectedQty** 和 **StockedQty** 從 [可用欄位]  拖曳至 [值]  方塊。  
  
    2.  按一下 [ **sum （ProductID）**]、[ **sum （PurchaseOrderID）**]、 **[sum （PurchaseOrderDetailID）**]、 **[sum （OrderQty）**]、 **[Sum （ReceivedQty）**]、 **[sum （RejectedQty）**] 和 [sum **（StockedQty）** ] 旁的箭號，並清除 [**總和**] 選取專案。  
  
7.  按兩次 **[下一步**]，然後按一下 **[完成**] 以關閉**報表精靈**。  
  
     現在您已建立 .rdlc 檔。 此檔案會在報表設計師中開啟。 您設計的 Tablix 現在會顯示於設計介面中。  
  
8.  在 .rdlc 檔開啟的情況下，執行下列操作加入參數：  
  
    1.  按一下 [**報表資料**] 窗格中的 [**參數**]，然後按一下 [**加入參數**]。  
  
    2.  在 [名稱]  方塊中，輸入 **productid**。  
  
    3.  確認已在 [資料類型]  清單方塊中，選取 [整數]  。  
  
    4.  按一下 [確定]  。  
  
9. 儲存 .rdlc 檔。  
  
## <a name="next-task"></a>下一項工作  
 您已使用 [報表精靈] 成功設計子報表。 接下來您要將 ReportViewer 控制項加入至網站應用程式。  
  
  
