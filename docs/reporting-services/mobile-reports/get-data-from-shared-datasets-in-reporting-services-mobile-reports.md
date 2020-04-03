---
title: 從 Reporting Services 行動報表中的共用資料集取得資料 | Microsoft Docs
description: SQL Server 行動報表發行工具可以使用 Reporting Services 入口網站上設定的共用資料來源，從幾乎任何來源存取資料。
ms.date: 03/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: 0b846451-c8d0-412c-802d-a42bb1ff8c63
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b4cc5e1538d1575e05e1eecd3959c98404cdbf5d
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "79448242"
---
# <a name="get-data-from-shared-datasets-in-reporting-services-mobile-reports"></a>從 Reporting Services 行動報表中的共用資料集取得資料
除了[載入 Excel 檔案資料](../../reporting-services/mobile-reports/prepare-excel-data-for-reporting-services-mobile-reports.md)，SQL Server 行動報表發行工具也可以存取幾乎所有來源的資料。 存取資料需有共用的資料來源，在 Reporting Services 入口網站設定。 深入了解 [建立共用資料來源](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md) 和 [建立共用資料集](../../reporting-services/report-data/manage-shared-datasets.md)。  
  
在 Reporting Services 伺服器上設定共用的資料來源和共用的資料集之後，您可以將它們用在以 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] 建立的行動報表中。   
  
從 [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] 連接到 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)]伺服器之後，即可直接將行動報表連接到共用資料集。   
  
1. 在 **[資料]** 索引標籤上，選取 **[加入資料]** 。  
  
2. 選取 **[報表伺服器]** 。   
  
3.  如果這是第一次連接到伺服器，請填入伺服器名稱以及您的名稱和密碼。 在 [伺服器位址] 方塊中放入伺服器名稱，其格式如下：  
  
    \<"伺服器名稱">/reports/  
  
    在此範例中：  
       
    ![SSMRP_ConnectToServer](../../reporting-services/mobile-reports/media/ssmrp-connecttoserver.png)  
      
  
4. 當您選取 [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] 伺服器時，您會在資料夾中看到可用的資料集。 選取資料要匯入到 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)]的資料集。  
  
   ![SS_MRP_ServerData](../../reporting-services/mobile-reports/media/ss-mrp-serverdata.png)  
  
匯入資料集之後，您就可以像處理模擬資料，或是處理 Excel 檔案的本機資料一樣，設計自己的行動報表。  
  
共用資料集預設保持最新的資料，因為每次有人檢視以資料集為基礎的行動報表，SQL Server 就會執行基礎查詢，並傳回最新的資料。 您可以很清楚地看到，如果有許多人檢視您的行動報表，實在不太理想，所以，您可以設定定期執行查詢並快取結果資料集。 這篇部落格文章說明 [快取和資料重新整理如何在 Web 入口網站中運作](https://christopherfinlan.com/2016/02/10/so-refreshinghow-data-refresh-works-with-mobile-reports-and-kpis-in-reporting-services/)。  
  
## <a name="add-edit-or-remove-a-report-server"></a>加入、編輯或移除報表伺服器  
  
如果您已連線到報表伺服器，當您選取 [資料] 索引標籤中的 [新增資料]  時，您不會看到新增其他報表伺服器的選項。 請改為遵循下列步驟。  
  
1. 選取左上角的 [連線]  。  
  
   ![SSMRP_AddConnectionIcon](../../reporting-services/mobile-reports/media/ssmrp-addconnectionicon.png)  
     
   隨即會在右側開啟 [伺服器連接] 窗格。  
     
   ![SSMRP_ServerConnectnPane](../../reporting-services/mobile-reports/media/ssmrp-serverconnectnpane.png)  
     
2. 加入新的伺服器連接，或是編輯或移除現有的連接。  
  
### <a name="see-also"></a>另請參閱  
- [使用 SQL Server 行動報表發行工具建立與發行行動報表](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
-  [入口網站 (SSRS 原生模式)](../../reporting-services/web-portal-ssrs-native-mode.md)  
-  在 [iPad app 中檢視 SQL Server 行動報表和 KPI](https://pbiwebprod-docs.azurewebsites.net/documentation/powerbi-mobile-ipad-kpis-mobile-reports)  (Power BI for iOS)  
-  請參閱 [在 iPhone 應用程式中檢視 SQL Server 行動報表和 KPI (iOS 版 Power BI)](https://pbiwebprod-docs.azurewebsites.net/documentation/powerbi-mobile-iphone-kpis-mobile-reports) (iOS 版 Power BI)  
  
  
  
  

