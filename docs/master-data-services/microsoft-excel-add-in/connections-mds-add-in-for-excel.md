---
title: "連接 (適用於 Excel 的 MDS 增益集) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2f2b2f9d-7744-460e-83cd-56d34ea70ff0
caps.latest.revision: 12
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 12
---
# 連接 (適用於 Excel 的 MDS 增益集)
  若要將資料下載至 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]中，您必須先建立連接。 連接可讓 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] Web 服務知道要連接的目標 MDS 資料庫。  
  
 連接字串通常是 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式的 URL，例如 http://contoso/mds。  
  
 每次您啟動 Excel 時，都必須連接到 MDS 儲存機制。 唯一的例外狀況是使用中試算表已經包含 MDS 管理的資料。 在此情況中，每次您重新整理或發行工作表中的資料時，系統就會自動建立連接。  
  
 您可以建立多個連接。 最近存取的連接會被視為預設值。  
  
 多位使用者可以同時進行連接。 不過，當多位使用者嘗試發行相同的資料時，可能會引發衝突。 如需詳細資訊，請參閱[概觀：從 Excel 匯入資料 &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/overview-importing-data-from-excel-mds-add-in-for-excel.md)。  
  
## 自動連接並載入經常使用的資料  
 如果您想要永遠連接到相同的伺服器並且載入相同的資料集，可以建立包含連接和篩選資訊的捷徑查詢檔案。 如需查詢檔案的詳細資訊，請參閱[捷徑查詢檔案 &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/shortcut-query-files-mds-add-in-for-excel.md)。  
  
## Data Quality Services  
 [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] 具有 Data Quality Services 功能，可協助您在發行資料至 MDS 儲存機制之前比對資料。 當您建立連接時，如果 DQS 資料庫與 MDS 資料庫安裝在相同的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上，您就能夠在功能區上檢視 DQS 按鈕。 如果 DQS_Main 資料庫不存在執行個體上，系統就不會顯示這些按鈕，而且資料品質功能將無法使用。  
  
## 相關工作  
  
|工作描述|主題|  
|----------------------|-----------|  
|建立 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 資料庫的連接。|[連接到 MDS 儲存機制 &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/connect-to-an-mds-repository-mds-add-in-for-excel.md)|  
|將 MDS 資料載入 Excel 中。|[將資料從 Master Data Services 匯出至 Excel](../../master-data-services/microsoft-excel-add-in/export-data-to-excel-from-master-data-services.md)|  
|在將 MDS 資料載入 Excel 之前篩選資料。|[在匯出之前篩選資料 &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/filter-data-before-exporting-mds-add-in-for-excel.md)|  
  
## 相關內容  
  
-   [概觀：將資料匯出至 Excel &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/overview-exporting-data-to-excel-mds-add-in-for-excel.md)  
  
-   [捷徑查詢檔案 &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/shortcut-query-files-mds-add-in-for-excel.md)  
  
-   [適用於 Microsoft Excel 的 Master Data Services 增益集](../../master-data-services/microsoft-excel-add-in/master-data-services-add-in-for-microsoft-excel.md)  
  
  