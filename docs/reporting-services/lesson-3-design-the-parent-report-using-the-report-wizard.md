---
title: "第 3 課：使用報表精靈設計父報表 | Microsoft Docs"
ms.custom: ""
ms.date: "05/18/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 2f69dcd3-cd6d-45a9-a62a-ba6f5f3179d8
caps.latest.revision: 9
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 9
---
# 第 3 課：使用報表精靈設計父報表
在您建立父報表的資料連接和資料表之後，下一步是要使用報表設計師中的 [報表精靈] 設計父報表。 如需報表設計師的詳細資訊，請參閱[使用報表設計師設計報表 &#40;SSRS&#41;](../reporting-services/tools/design-reports-with-report-designer-ssrs.md)。  
  
### 若要使用報表精靈設計父報表  
  
1.  請確認已在**方案總管**中選取頂層網站。  
  
2.  以滑鼠右鍵按一下網站，然後選取 [加入新項目]。  
  
3.  在 [加入新項目] 對話方塊中，按一下 [報表精靈]，輸入報表檔案的名稱，然後按一下 [加入]。  
  
    這樣會啟動 [報表精靈]。  
  
4.  在 [資料集屬性] 頁面的 [資料來源] 方塊中，選取您在[第 2 課：定義父報表的資料連接和資料表](../reporting-services/lesson-2-define-a-data-connection-and-data-table-for-parent-report.md)中建立的 [DataSet1]。  
  
    [可用資料集] 方塊會自動更新為您如上所建立的 **DataTable**。  
  
5.  選取 **[下一步]**。  
  
6.  在 [排列欄位] 頁面中執行下列操作：  
  
    1.  從 [可用欄位] 將 **ProductID**、**Name**、**ProductNumber**、**SafetyStockLevel** 和 **ReorderLevel** 拖曳至 [值] 方塊。  
  
    2.  按一下 **Sum(ProductID)**、**Sum(SafetyStockLevel)**、**Sum(ReorderLevel)** 旁的箭頭，並清除 **Sum** 選項。  
  
7.  連選兩次 [下一步]，然後選取 [完成] 關閉 [報表精靈]。  
  
    現在您已建立 .rdlc 檔。 此檔案會在報表設計師中開啟。 您設計的 Tablix 現在會顯示於設計介面中。  
  
8.  儲存 .rdlc 檔。  
  
## 下一項工作  
您已使用 [報表精靈] 成功設計父報表。 接下來您將建立子報表的資料連接和資料表。 請參閱[第 4 課：定義子報表的資料連接和資料表](../reporting-services/lesson-4-define-a-data-connection-and-data-table-for-child-report.md)。  
  
  
  
