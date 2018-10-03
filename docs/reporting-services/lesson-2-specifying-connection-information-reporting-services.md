---
title: 第 2 課：指定連線資訊 (Reporting Services) | Microsoft Docs
ms.date: 05/23/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 54405a3a-d7fa-4d95-8963-9aa224e5901e
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 381192f80128ca3bd2ebade55dc539137c4bc9bd
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47805606"
---
# <a name="lesson-2-specifying-connection-information-reporting-services"></a>第 2 課：指定連接資訊 (Reporting Services)
將  分頁報表報表新增至教學課程專案第 1 課之後，您需要定義 *「資料來源」*[!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)]，這是讓報表從關聯式資料庫、多維度資料庫或其他來源存取資料所用的連線資訊。  
  
在這一課，您將使用 [!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] 範例資料庫作為您的資料來源。 本教學課程假設這個資料庫是位於安裝在本機電腦的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] 預設執行個體中。  
  
### <a name="to-set-up-a-connection"></a>設定連接  
  
1.  在 [報表資料] 窗格中，按一下 [新增]，然後按一下 [資料來源]。  
如果看不到 [報表資料] 窗格，請按一下 [檢視] 功能表上的 [報表資料]。  

    ![ssrs-table-tutorial-2-new-data-source](../reporting-services/media/ssrs-table-tutorial-2-new-data-source.png)
  
   2.  在 [名稱] 中，鍵入 *Adventureworks2014*。  
  
3.  確認 [內嵌連接] 已選取。  
  
4.  在 [類型] 中，選取 [Microsoft SQL Server]。  
  
5.  在 [連接字串] 中，鍵入下列字串：  
  
    ```  
    Data source=localhost; initial catalog=AdventureWorks2014  
    ```  
  
     這個連接字串假設 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]、報表伺服器和 [!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] 資料庫都安裝在本機電腦上，且您有登入 [!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] 資料庫的權限。 如果您的 AdventureWorks2014 資料庫不在本機電腦上，請變更連接字串，並以您的資料庫伺服器執行個體名稱取代 *loclahost*。
  
     >[!NOTE]  
    >如果您使用 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] with Advanced Services 或具名執行個體，則連接字串必須包括執行個體資訊：  
    >  
    >`Data source=localhost\SQLEXPRESS; initial catalog=AdventureWorks2014`  
    >  
    >如需連接字串的詳細資訊，請參閱： [報表產生器中的資料連接、資料來源及連接字串](../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)。  
     
  
6.  按一下左窗格中的 [認證]，然後按一下 [使用 Windows 驗證 (整合式安全性)]。  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)] 資料來源 **AdventureWorks2014** 會新增至 [報表資料] 窗格。  
![ssrs_adventureworks_datasource](../reporting-services/media/ssrs-adventureworks-datasource.png)  
## <a name="next-task"></a>下一項工作  
您已順利定義 [!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] 範例資料庫的連接。 下一步，您將建立報表。 請參閱[第 3 課：定義資料表報表的資料集 &#40;Reporting Services&#41;](../reporting-services/lesson-3-defining-a-dataset-for-the-table-report-reporting-services.md)。  
  
## <a name="see-also"></a>另請參閱  
[報表產生器中的資料連接、資料來源及連接字串](../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
  
  
  

