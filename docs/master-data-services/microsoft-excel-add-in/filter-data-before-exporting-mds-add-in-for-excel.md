---
title: "（MDS 增益集適用於 Excel） 匯出之前先篩選資料 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9e30eae0-776b-4a09-aac3-0c0249d92ca5
caps.latest.revision: 10
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 10
---
# （MDS 增益集適用於 Excel） 匯出之前先篩選資料
  在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], ，篩選資料，當您想要限制的大小或匯出到 Excel 的資料範圍。  
  
## 必要條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[總管]** 功能區域的權限。  
  
### 若要在匯出之前篩選資料  
  
1.  開啟 Excel 並在 **主要資料** 索引標籤上，連接到 MDS 儲存機制。 如需詳細資訊，請參閱 [連接到 MDS 儲存機制 & #40。MDS 增益集的 Excel & #41;](../../master-data-services/microsoft-excel-add-in/connect-to-an-mds-repository-mds-add-in-for-excel.md)。  
  
2.  在 **主資料總管** ] 窗格中，選取模型和版本。 系統就會填入實體的清單。  
  
    -   如果 **主資料總管** ] 窗格中不會顯示， **連接和載入** 群組中，按一下 **顯示總管**。  
  
    -   如果 **主資料總管** 窗格已停用，這是因為現有的工作表已經包含 MDS 管理的資料。 若要啟用此窗格，請開啟新的工作表。  
  
3.  在 **主資料總管** 窗格的實體清單中，按一下您想要篩選的實體。  
  
4.  在功能區中，在 **連接和載入** 群組中，按一下 **篩選**。  
  
5.  完成 **篩選** ] 對話方塊中選取要顯示的屬性 （資料行），設定資料行的順序和必要時，篩選資料以傳回較少的資料列。 檢視 **摘要** 窗格將會傳回多少資料。 如需詳細資訊，請參閱 [篩選對話方塊 & #40。MDS 增益集的 Excel & #41;](../../master-data-services/microsoft-excel-add-in/filter-dialog-box-mds-add-in-for-excel.md)。  
  
6.  按一下 [ **資料載入**。 工作表就會填入 MDS 管理的資料。  
  
    > [!NOTE]  
    >  -   只有前 1 百萬個成員會載入 Excel 中。  
    > -   在屬於受條件約束之清單 (網域屬性) 的資料行中，預設只會載入前 25,000 個值。  
  
## 後續步驟  
 [從 Excel 將資料匯入至 Master Data Services & #40。MDS 增益集的 Excel & #41;](../../master-data-services/microsoft-excel-add-in/import-data-from-excel-to-master-data-services-mds-add-in-for-excel.md)  
  
## 另請參閱  
 [概觀︰ 將資料匯出至 Excel & #40。MDS 增益集的 Excel & #41;](../../master-data-services/microsoft-excel-add-in/overview-exporting-data-to-excel-mds-add-in-for-excel.md)   
 [篩選對話方塊 & #40。MDS 增益集的 Excel & #41;](../../master-data-services/microsoft-excel-add-in/filter-dialog-box-mds-add-in-for-excel.md)   
 [重新排列欄 & #40。MDS 增益集的 Excel & #41;](../../master-data-services/microsoft-excel-add-in/reorder-columns-mds-add-in-for-excel.md)  
  
  