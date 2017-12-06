---
title: "將參數新增至行動報表 | Reporting Services | Microsoft Docs"
ms.custom: 
ms.date: 11/01/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: mobile-reports
ms.reviewer: 
ms.suite: pro-bi
ms.technology: reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 113cb057-deec-40eb-abc8-f35d3900eaa6
caps.latest.revision: "12"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 120d86d046a3be19e179b9b27edc20ba3b044a9e
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="add-parameters-to-a-mobile-report--reporting-services"></a>將參數加入行動報表中 | Reporting Services
您可以使用參數建立 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 行動報表，讓您和您報表的讀者可以篩選報表。 使用參數的報表也可以是 [從來源報表鑽研](../../reporting-services/mobile-reports/add-drillthrough-from-a-mobile-report-to-other-mobile-reports-or-urls.md)的目標。 

若要使用參數建立行動報表，請從至少包含一個參數的共用資料集開始。 請參閱 [在共用資料集中建立參數](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)。  

將參數加入行動報表之後，您可以建立 URL 以 [使用查詢字串參數開啟報表](../../reporting-services/mobile-reports/open-a-mobile-report-with-specific-query-string-parameters-reporting-services.md)。

1. 在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion.md)] Web 入口網站的頂端列中，選取 [新增] > [行動報表]。  
  
   ![PBI_SSMRP_NewMenu](../../reporting-services/mobile-reports/media/pbi-ssmrp-newmenu.png)  
     
2. 選取 [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)] 左上角的 [資料] 索引標籤。   
  
3. 選取右上角的 [新增資料]。  
  
4. 選取 [報表伺服器]，然後選取伺服器。  
  
5. 瀏覽至伺服器上的共用資料集，然後選取具有參數的伺服器。  
  
   在方格中，您會看到資料集中的資料。 具有中括弧 **{ }** 的綠色圓形標記具有參數的資料集。  
     
   ![SSMRP_PforParam](../../reporting-services/mobile-reports/media/ssmrp-pforparam.png)  
  
6. 選取索引標籤上的齒輪，然後選取 **Param {}**。  
  
   ![SSMRP_ParamWheel](../../reporting-services/mobile-reports/media/ssmrp-paramwheel.png)  
  
7. 選取會將值傳遞給參數的報表元素。  
  
   ![SSMRP_SetParam](../../reporting-services/mobile-reports/media/ssmrp-setparam.png)  
     
8. 選取 [預覽] 查看報表的外觀。 在此報表中，選擇清單使用類別目錄參數。

   ![sql-server-mobile-report-publisher-Selection-List-View-No-Selection](../../reporting-services/mobile-reports/media/sql-server-mobile-report-publisher-selection-list-view-no-selection.png) 
   
9. 當您在選擇清單中選取值時，會將報表篩選為只顯示該值。在此案例中為「附屬應用程式」。

   ![sql-server-mobile-report-publisher-Selection-List-Category-Selected](../../reporting-services/mobile-reports/media/sql-server-mobile-report-publisher-selection-list-category-selected.png)   
  
### <a name="see-also"></a>另請參閱  
-  [使用特定查詢字串參數開啟行動報表](../../reporting-services/mobile-reports/open-a-mobile-report-with-specific-query-string-parameters-reporting-services.md)
-  [從行動報表將鑽研加入其他行動報表或 URL](../../reporting-services/mobile-reports/add-drillthrough-from-a-mobile-report-to-other-mobile-reports-or-urls.md)
-  [建立共用或內嵌的資料集](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)
- [使用 SQL Server 行動報表發行工具建立與發行行動報表](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
  
  

