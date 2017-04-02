---
title: "重新排序資料行 (適用於 Excel 的 MDS 增益集) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ac00462e-c0f7-4b8d-86f2-d9eda2598a15
caps.latest.revision: 7
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 7
---
# 重新排序資料行 (適用於 Excel 的 MDS 增益集)
  在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], ，可以載入之前篩選清單重新排列資料行。  
  
 當您重新排序屬性中的 **篩選** 對話方塊中，將資料載入至 Excel 時使用新的順序。 不過，下次您篩選屬性資料時，此順序將會回復到原始設計的順序。 若要永久變更順序，系統管理員應該變更的順序 **系統管理** 區域的主資料管理員。 如需詳細資訊，請參閱 [變更屬性的順序](../../master-data-services/change-the-order-of-attributes.md)。  
  
## 必要條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[總管]** 功能區域的權限。  
  
### 若要重新排序 MDS 管理的資料行  
  
1.  開啟 Excel 並在 **主要資料** 索引標籤上，連接到 MDS 儲存機制。 如需詳細資訊，請參閱 [連接到 MDS 儲存機制 & #40。MDS 增益集的 Excel & #41;](../../master-data-services/microsoft-excel-add-in/connect-to-an-mds-repository-mds-add-in-for-excel.md)。  
  
2.  在 **主資料總管** ] 窗格中，選取模型和版本。 系統就會填入實體的清單。  
  
    -   如果 **主資料總管** ] 窗格中不會顯示， **連接和載入** 群組中，按一下 **顯示總管**。  
  
    -   如果 **主資料總管** 窗格已停用，這是因為現有的工作表已經包含 MDS 管理的資料。 若要啟用此窗格，請開啟新的工作表。  
  
3.  在 **主資料總管** 窗格中，按一下實體。  
  
4.  在 **連接和載入** 群組中，按一下 **篩選**。  
  
5.  在 **篩選** 對話方塊中，於 **資料行** 區段中的，在屬性清單中按一下您想要移動的屬性。  
  
6.  右邊的清單，按一下 [ **總** 或 **下** 箭號以移動保留的屬性工作表中以滑鼠右鍵。  
  
7.  針對每個屬性重複步驟 7，直到由上至下順序代表您想要在工作表中呈現的由左至右順序為止。  
  
8.  按一下 [ **資料載入**。 工作表就會填入 MDS 管理的資料，而且資料行會依照您所指定的順序顯示。  
  
## 另請參閱  
 [概觀︰ 將資料匯出至 Excel & #40。MDS 增益集的 Excel & #41;](../../master-data-services/microsoft-excel-add-in/overview-exporting-data-to-excel-mds-add-in-for-excel.md)  
  
  