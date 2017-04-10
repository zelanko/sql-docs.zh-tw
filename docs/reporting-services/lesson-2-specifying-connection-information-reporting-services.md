---
title: "第 2 課：指定連接資訊 (Reporting Services) | Microsoft Docs"
ms.custom: ""
ms.date: "05/23/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 54405a3a-d7fa-4d95-8963-9aa224e5901e
caps.latest.revision: 53
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 51
---
# 第 2 課：指定連接資訊 (Reporting Services)
將報表加入教學課程專案之後，您需要定義「資料來源」，這是讓報表從關聯式資料庫、多維度資料庫或其他資源存取資料所用的連接資訊。  
  
在這一課，您將使用 [!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] 範例資料庫作為您的資料來源。 本教學課程假設這個資料庫位於本機電腦上安裝的預設 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] 執行個體中。  
  
### 設定連接  
  
1.  在 [報表資料] 窗格中，按一下 [新增]，然後按一下 [資料來源…]。  
如果看不到 [報表資料] 窗格，請按一下 [檢視] 功能表上的 [報表資料]。  
  
   2.  在 [名稱] 中，輸入 *Adventureworks2014*。  
  
3.  確認 [內嵌連接] 已選取。  
  
4.  在 [類型] 中，選取 [Microsoft SQL Server]。  
  
5.  在 [連接字串] 中，輸入下列字串：  
  
    ```  
    Data source=localhost; initial catalog=AdventureWorks2014  
    ```  
  
這個連接字串假設 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]、報表伺服器和 [!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] 資料庫都安裝在本機電腦上，且您有登入 [!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] 資料庫的權限。 如果您的 AdventureWorks2014 資料庫不在本機電腦上，請變更連接字串，並以您的資料庫伺服器執行個體名稱取代 *loclahost*。
   
  
 > [!NOTE]  
 > 如果您使用 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] with Advanced Services 或具名執行個體，則連接字串必須包括執行個體資訊：  
 >   
 > `Data source=localhost\SQLEXPRESS; initial catalog=AdventureWorks2014`  
 >   
 > 如需連接字串的詳細資訊，請參閱：  
 > *  [Data Connections, Data Sources, and Connection Strings in Reporting Services](../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
    > * [資料來源屬性對話方塊、一般](../Topic/Data%20Source%20Properties%20Dialog%20Box,%20General.md)  
        
  
6.  按一下左窗格中的 [認證]，然後按一下 [使用 Windows 驗證 (整合式安全性)]。  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)] 資料來源 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 會加入 [報表資料] 窗格。  
![ssrs_adventureworks_datasource](../reporting-services/media/ssrs-adventureworks-datasource.png)  
## 下一項工作  
您已順利定義 [!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] 範例資料庫的連接。 下一步，您將建立報表。 請參閱[第 3 課：定義資料表報表的資料集 &#40;Reporting Services&#41;](../reporting-services/lesson-3-defining-a-dataset-for-the-table-report-reporting-services.md)。  
  
## 另請參閱  
[資料來源屬性對話方塊、一般](../Topic/Data%20Source%20Properties%20Dialog%20Box,%20General.md)  
[Data Connections, Data Sources, and Connection Strings in Reporting Services](../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
  
  
  
