---
title: "結合資料 (適用於 Excel 的 MDS 增益集) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a867dc15-5a0d-457c-8304-ac323bcf9377
caps.latest.revision: 6
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 6
---
# 結合資料 (適用於 Excel 的 MDS 增益集)
  在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], ，結合兩個工作表的資料，當您想要發行前比較資料。 在此程序中，將兩個工作表中的資料結合為一個工作表。 然後可以進一步進行比較，並判斷哪些資料 (如果有) 將發行到 MDS 儲存機制。  
  
## 必要條件  
  
-   您必須擁有包含 MDS 管理之資料的工作表。 如需詳細資訊，請參閱 [資料匯出至 Excel 的 Master Data Services](../../master-data-services/microsoft-excel-add-in/export-data-to-excel-from-master-data-services.md)。  
  
-   您必須擁有另一個工作表，其資料將要與 MDS 管理之資料結合。 此工作表必須具有標頭資料列。  
  
### 若要將非管理的資料合併到 MDS 管理的工作表中  
  
1.  在包含 MDS 管理的資料工作表上 **發行和驗證** 群組中，按一下 **結合資料**。  
  
2.  在 **結合資料** 對話方塊旁 **要與 MDS 資料結合的範圍** 文字] 方塊中，按一下圖示。 此對話方塊會收縮。  
  
3.  按一下包含您要結合之資料的工作表。  
  
4.  反白顯示工作表上要結合的所有資料格，包括標頭資料列。  
  
5.  在 **結合資料** 對話方塊方塊中，按一下圖示。 此對話方塊會展開。  
  
6.  針對列出的 MDS 實體選取底下的資料行的資料行 **對應資料行**。 並不是所有 MDS 資料行都需要對應資料行。  
  
7.  按一下 [ **結合**。 A **來源** 會顯示資料行，指出資料是否來自 MDS 或外部來源。  
  
## 後續步驟  
  
-   若要尋找 MDS 管理與外部資料之間的相似之處，請參閱 [比對相似資料 & #40。MDS 增益集的 Excel & #41;](../../master-data-services/microsoft-excel-add-in/match-similar-data-mds-add-in-for-excel.md)。  
  
## 另請參閱  
 [概觀︰ 將資料匯出至 Excel & #40。MDS 增益集的 Excel & #41;](../../master-data-services/microsoft-excel-add-in/overview-exporting-data-to-excel-mds-add-in-for-excel.md)   
 [適用於 Excel 的 MDS 增益集中的資料品質比對](../../master-data-services/microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md)  
  
  