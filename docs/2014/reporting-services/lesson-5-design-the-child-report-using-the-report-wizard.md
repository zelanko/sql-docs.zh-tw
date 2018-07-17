---
title: 第 5 課：使用報表精靈設計子報表 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 19a3f927-ea97-4f40-a5f8-cd5f2598e4da
caps.latest.revision: 6
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 712e454c9bc89fd1df8584789ec9c25796748201
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37294168"
---
# <a name="lesson-5-design-the-child-report-using-the-report-wizard"></a>第 5 課：使用報表精靈設計子報表
  在您建立子報表的資料連接和資料表之後，下一步是要使用報表設計師中的 [報表精靈] 設計子報表。 如需報表設計師的詳細資訊，請參閱[使用報表設計師設計報表 &#40;SSRS&#41;](tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md)。  
  
### <a name="to-design-the-child-report-using-the-report-wizard"></a>若要使用報表精靈設計子報表  
  
1.  請確認已在 **方案總管**中選取頂層網站。  
  
2.  以滑鼠右鍵按一下網站，然後選取 [新增項目]。  
  
3.  在 [**加入新項目**] 對話方塊中，按一下**報表精靈**，輸入報表檔的名稱，然後按一下**新增**。  
  
     這樣會啟動 [報表精靈]。  
  
4.  在 **資料集屬性**頁面上，於**資料來源**方塊中，按一下**DataSet2**。  
  
     [可用資料集] 方塊會自動更新為您所建立的 DataTable。  
  
5.  按 [下一步] 。  
  
6.  在 [排列欄位] 頁面中執行下列操作：  
  
    1.  將 **ProductID**、**PurchaseOrderID**、**PurchaseOrderDetailID**、**OrderQty**、**ReceivedQty**、**RejectedQty** 和 **StockedQty** 從 [可用欄位] 拖曳至 [值] 方塊。  
  
    2.  按一下箭號旁**sum （productid)**， **sum （purchaseorderid)**， **sum （purchaseorderdetailid)**， **sum （orderqty)**， **Sum （receivedqty)**， **sum （rejectedqty)**，以及**sum （stockedqty)** 清除**總和**選取項目。  
  
7.  按一下 [**下一步]** 兩次，然後按一下**完成**以關閉**報表精靈**。  
  
     現在您已建立 .rdlc 檔。 此檔案會在報表設計師中開啟。 您設計的 Tablix 現在會顯示於設計介面中。  
  
8.  在 .rdlc 檔開啟的情況下，執行下列操作加入參數：  
  
    1.  按一下 **參數**中**報表資料**窗格中，然後再按一下**將參數加入**。  
  
    2.  在 [名稱] 方塊中，輸入 **productid**。  
  
    3.  確認已在 [資料類型] 清單方塊中，選取 [整數]。  
  
    4.  按一下 [確定] 。  
  
9. 儲存 .rdlc 檔。  
  
## <a name="next-task"></a>下一項工作  
 您已使用 [報表精靈] 成功設計子報表。 接下來您要將 ReportViewer 控制項加入至網站應用程式。  
  
  
