---
title: "建立 Reporting Services 行動報表 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e84dc855-aede-4fb4-b721-e6d8787961f4
caps.latest.revision: 10
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 10
---
# 建立 Reporting Services 行動報表
您可以使用 [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)]，在可調整格線資料列和資料行且具有彈性行動報表元素的設計介面上，快速建立適用於任何畫面大小的 [!INCLUDE[PRODUCT_NAME](../../includes/sscurrent.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion.md)] 行動報表。  
  
第一次建立行動報表時，您可以從 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion.md)] Web 入口網站，將 [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-short.md)] 安裝在本機電腦上。 您可以從 [Microsoft 下載中心](http://go.microsoft.com/fwlink/?LinkID=733527)進行安裝。 之後，您就可以從入口網站或本機啟動。   
    
1. 在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion.md)] Web 入口網站的頂端列中，選取 [新增] > [行動報表]。  
  
   ![PBI_SSMRP_NewMenu](../../reporting-services/mobile-reports/media/pbi-ssmrp-newmenu.png)  
     
2. 在 [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-short.md)] 的 [配置] 索引標籤中，選取導覽器、量測計、圖表、地圖或資料格，然後將其拖曳到設計格線。  
  
3. 按住元素的右下角，將其拖曳成您想要的大小。  
  
   ![SSMRP_ResizeChart](../../reporting-services/mobile-reports/media/ssmrp-resizechart.png)  
  
   這是**主要**設計格線，您可以在此建立報表中要出現的元素。 稍後，您可以[為平板電腦或手機進行配置](../../reporting-services/mobile-reports/lay-out-a-reporting-services-mobile-report-for-phone-or-tablet.md)。     
     
   在設計格線下方的**視覺屬性**中，請注意您可以設定的各種屬性。  
     
4. 選取左上角的 [資料] 索引標籤，即可看到其中已經有相關模擬資料的圖表。   
  
   ![SSMRP_SimTable](../../reporting-services/mobile-reports/media/ssmrp-simtable.png)  
  
5. 選取右上角的 [加入資料]。  
  
6. 選取 [本機 Excel] 或 [報表伺服器]。  
  
   >**提示**︰若您要從 Excel 加入資料，請務必︰  
    >* [準備好 Excel 資料](../../reporting-services/mobile-reports/prepare-excel-data-for-reporting-services-mobile-reports.md)以便在行動報表中使用。  
    >* 請先關閉檔案。  
7. 選取想要的工作表，然後選取 [匯入]。   
   您可以從活頁簿一次加入多個工作表。  
    
     ![SSMRP_AddExcelData](../../reporting-services/mobile-reports/media/ssmrp-addexceldata.png)  
  
8. 在 [資料] 索引標籤的 [資料屬性] 方塊中，選取要出現在圖表中的資料表及欄位。  
  
   ![SSMRP_DataProps](../../reporting-services/mobile-reports/media/ssmrp-dataprops.png)  
  
9. 回到 [配置] 索引標籤，您可以在 [視覺效果屬性] 方塊中設定屬性，例如**標題**、**時間單位**及**數值格式**。  
  
   ![SSMRP_ChartVizProps](../../reporting-services/mobile-reports/media/ssmrp-chartvizprops.png)  
    
10. 選取左上方的 [預覽] 可查看報表的成形情況。  
  
11. 是時候儲存報表了。 選取左上方的儲存圖示，然後選取 [儲存至本機] 或 [儲存至伺服器]。  
  
   您需要有 [!INCLUDE[PRODUCT_NAME](../../includes/sscurrent.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion.md)] 報表伺服器的存取權，才能將其儲存至伺服器。  
     
   ### 另請參閱  
     
-   [使用 SQL Server 行動報表發行工具建立與發行行動報表](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
-   [為手機或平板電腦配置 Reporting Services 行動報表](../../reporting-services/mobile-reports/lay-out-a-reporting-services-mobile-report-for-phone-or-tablet.md)  
  
   