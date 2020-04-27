---
title: 升級 Master Data Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 9c3543f3-3eb9-455d-a9bf-f17e9506ad21
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: da78f21c6346281dc23332f40e8e6f46ff07aa06
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62774652"
---
# <a name="upgrade-master-data-services"></a>升級 Master Data Services
  升級至 Microsoft [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CTP2 的情況有四種。 請選擇最適合您情況的情況。  
  
-   [升級但不包含 Database Engine 升級](#noengine)  
  
-   [升級且包含 Database Engine 升級](#engine)  
  
-   [在兩部電腦的情況下升級](#twocomputer)  
  
-   [從備份還原資料庫的升級](#restore)  
  
> [!IMPORTANT]
>  -   不支援從 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CTP1 版本升級到 CTP2 版本。  
> -   在執行任何升級之前備份您的資料庫。  
> -   升級程序會重新建立預存程序，並升級 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]使用的資料表。 您對這些元件所做的任何自訂可能會遺失。  
> -   模型部署封裝只能在之前建立這些封裝的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本中使用。 您無法[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] / [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]將中建立的模型部署封裝[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]部署到。  
> -   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 將 Master Data Services 和 Data Quality Services 升級為 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CTP2 之後，您可以繼續使用  SP1 版適用於 Excel 的 Master Data Services 增益集。 不過，在升級為 SQL Server 2014 CTP2 之後，任何舊版適用於 Excel 的 Master Data Services 增益集將無法運作。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 您可以在 [這裡](https://go.microsoft.com/fwlink/?LinkId=328664)下載  SP1 版適用於 Excel 的 Master Data Services 增益集。  
  
##  <a name="upgrade-without-database-engine-upgrade"></a><a name="noengine"></a>升級但不升級資料庫引擎  
 此案例可視為並存[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] / [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]安裝，因為和[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]都是以平行方式安裝在同一部電腦或不同的電腦上。  
  
 在此情況下，您會繼續使用 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 主控您的 MDS 資料庫。 但是，您必須升級 MDS 資料庫的結構描述，然後建立 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Web 應用程式以存取 MDS 資料庫。 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Web 應用程式無法再存取 MDS 資料庫。  
  
 如果您選擇在同一[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]部電腦上安裝和舊版的[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]/[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]SQL Server （），您可以這樣做，因為檔案會安裝在不同的位置。  
  
-   根據預設，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中，檔案會安裝到 *磁碟機*:\Program Files\Microsoft SQL Server\120\Master Data Services。  
  
-   根據預設，在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]中，檔案會安裝到 *磁碟機*:\Program Files\Microsoft SQL Server\110\Master Data Services。  
  
-   根據預設，在 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]中，檔案會安裝到 *磁碟機*:\Program Files\Microsoft SQL Server\Master Data Services。  
  
 若要執行此工作，請完成下列步驟。  
  
1.  安裝 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 及您想要的其他任何功能。  
  
    1.  開啟 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安裝程式精靈。  
  
    2.  按一下左窗格中的 [安裝]****。  
  
    3.  按一下右窗格中的 [新增 SQL Server 獨立安裝或將功能加入至現有安裝]****。  
  
    4.  在 [功能選擇]**** 頁面上，選取 [[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]]**** 以及您想要安裝的其他任何功能。  
  
    5.  完成精靈。  
  
2.  在安裝完成後，升級 MDS 資料庫結構描述。  
  
    1.  開啟 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版的 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]。  
  
        > [!IMPORTANT]  
        >  若要升級 MDS 資料庫結構描述，您必須以建立 MDS 資料庫時指定之系統管理員帳戶的身分登入。 在 MDS 資料庫的 mdm.tblUser 中，這位使用者的 [識別碼]**** 值為 **1**。 如需變更此使用者的詳細資訊，請參閱[將系統管理員帳戶變更 &#40;Master Data Services&#41;](../../master-data-services/change-the-system-administrator-account-master-data-services.md)。  
  
    2.  按一下左窗格中的 [資料庫組態]  。  
  
    3.  在右窗格中，按一下 [**選取資料庫**]，然後指定[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]或[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]資料庫實例的資訊。  
  
    4.  按一下 [升級資料庫]  可啟動 [升級資料庫精靈]  。 如需詳細資訊，請參閱[升級資料庫精靈 &#40;Master Data Services 組態管理員&#41;](../../master-data-services/upgrade-database-wizard-master-data-services-configuration-manager.md)。  
  
3.  升級完成後，請建立 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Web 應用程式。  
  
    1.  開啟 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版的 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]。  
  
    2.  按一下左窗格中的 **[Web 組態]** 。  
  
    3.  從右窗格的 [網站]  清單中，選取下列其中一個選項：  
  
        -   [預設的網站]  ，然後按一下 [建立應用程式]  。  
  
        -   [建立新的網站]  。 建立網站時，便會自動建立新的 Web 應用程式。  
  
        > [!IMPORTANT]  
        >  在 SQL Server 2014 版的 Master Data Services 組態管理員中，可讓您選取您在舊版 SQL Server ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) 中的現有 MDS Web 應用程式。 您絕不能選取現有的 Web 應用程式，而是必須建立 MDS 的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Web 應用程式。 否則，當您嘗試將 Web 應用程式與升級的 MDS 資料庫建立關聯時，將會收到錯誤，說明因為該頁面的相關組態資料無效，所以無法存取所要求的頁面。  
        >   
        >  如果您要為 MDS Web 應用程式使用相同的名稱 (別名) 做為現有 ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) Web 應用程式，您必須先將 Web 應用程式和相關聯的應用程式集區從 IIS 刪除，然後使用 SQL Server 2014 版的 Master Data Services 組態管理員，以相同的名稱建立 Web 應用程式。 如需從 IIS 移除 Web 應用程式和應用程式集區的資訊，請參閱 [移除應用程式 (IIS)](https://go.microsoft.com/fwlink/?LinkId=323537) 和 [移除應用程式集區 (IIS)](https://go.microsoft.com/fwlink/?LinkId=323538)。  
  
4.  現在將新的 Web 應用程式與升級的 MDS 資料庫建立關聯。  
  
    1.  在 [建立應用程式與資料庫間的關聯]  區段中，按一下 [選取]  。  
  
    2.  選取 MDS 資料庫。  
  
    3.  按一下 [套用]  。  
  
##  <a name="upgrade-with-database-engine-upgrade"></a><a name="engine"></a> 升級且包含 Database Engine 升級  
 在此案例中，您要將資料庫引擎和 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 應用程式從 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 或 SQL Server 2012 升級到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 若要執行此工作，請完成下列步驟。  
  
1.  **僅適用於 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]** ：開啟 [控制台]   > [程式和功能]  ，並解除安裝 Microsoft [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)][!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]。  
  
2.  將資料庫引擎升級至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
    1.  開啟 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安裝程式精靈。  
  
    2.  按一下左窗格中的 [安裝]****。  
  
    3.  在右窗格中，按一下 [**從 SQL Server 2005]、[SQL Server 2008]、[SQL Server 2008 R2] 或 [SQL Server 2012**]。  
  
    4.  完成精靈。  
  
3.  **僅[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]適用于**：升級完成時，請新增**[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]** 功能。  
  
    1.  開啟 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安裝程式精靈。  
  
    2.  按一下左窗格中的 [安裝]****。  
  
    3.  按一下右窗格中的 [新增 SQL Server 獨立安裝或將功能加入至現有安裝]****。  
  
    4.  在嚮導的 [**安裝類型**] 頁面上，選取 [**將功能加入到現有的實例**] 選項，然後選擇要安裝 MDS 資料庫的實例。  
  
    5.  在 [**特徵選取**] 頁面的 [**共用功能**] **[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]** 底下，選取。  
  
    6.  完成精靈。  
  
4.  升級 MDS 資料庫結構描述。  
  
    1.  開啟 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版的 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]。  
  
        > [!IMPORTANT]  
        >  若要升級 MDS 資料庫結構描述，您必須以建立 MDS 資料庫時指定之系統管理員帳戶的身分登入。 在 MDS 資料庫的 mdm.tblUser 中，這位使用者的 [識別碼]**** 值為 **1**。 如需變更此使用者的詳細資訊，請參閱[將系統管理員帳戶變更 &#40;Master Data Services&#41;](../../master-data-services/change-the-system-administrator-account-master-data-services.md)。  
  
    2.  按一下左窗格中的 [資料庫組態]****。  
  
    3.  在右窗格中，按一下 [**選取資料庫**]，然後指定資料庫實例的資訊。  
  
    4.  按一下 [升級資料庫]**** 可啟動 [升級資料庫精靈]****。 如需詳細資訊，請參閱[升級資料庫精靈 &#40;Master Data Services 組態管理員&#41;](../../master-data-services/upgrade-database-wizard-master-data-services-configuration-manager.md)。  
  
    5.  按一下 [套用]  。  
  
5.  升級完成後，請建立 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Web 應用程式。  
  
    1.  開啟 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版的 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]。  
  
    2.  按一下左窗格中的 **[Web 組態]**。  
  
    3.  從右窗格的 [網站]**** 清單中，選取下列其中一個選項：  
  
        -   [預設的網站]****，然後按一下 [建立應用程式]****。  
  
        -   [建立新的網站]****。 建立網站時，便會自動建立新的 Web 應用程式。  
  
        > [!IMPORTANT]  
        >  在 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 版的 Master Data Services 組態管理員中，可讓您選取您在舊版 SQL Server ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 或 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]) 中的現有 MDS Web 應用程式。 您絕不能選取現有的 Web 應用程式，而是必須建立 MDS 的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Web 應用程式。 否則，當您嘗試將 Web 應用程式與升級的 MDS 資料庫建立關聯時，將會收到錯誤，說明因為該頁面的相關組態資料無效，所以無法存取所要求的頁面。  
        >   
        >  如果您要為 MDS Web 應用程式使用相同的名稱 (別名) 做為現有 ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) Web 應用程式，您必須先將 Web 應用程式和相關聯的應用程式集區從 IIS 刪除，然後使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版的 Master Data Services 組態管理員，以相同的名稱建立 Web 應用程式。 如需從 IIS 移除 Web 應用程式和應用程式集區的資訊，請參閱 [移除應用程式 (IIS)](https://go.microsoft.com/fwlink/?LinkId=323537) 和 [移除應用程式集區 (IIS)](https://go.microsoft.com/fwlink/?LinkId=323538)。  
  
6.  現在將新的 Web 應用程式與升級的 MDS 資料庫建立關聯。  
  
    1.  在 [建立應用程式與資料庫間的關聯]**** 區段中，按一下 [選取]****。  
  
    2.  選取 MDS 資料庫。  
  
    3.  按一下 [套用]  。  
  
##  <a name="upgrade-in-two-computer-scenario"></a><a name="twocomputer"></a> 在兩部電腦的情況下升級  
 此情況包括升級在兩部電腦上安裝 SQL Server 的系統：一部安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，另一部安裝 SQL Server 2008 R2 或 SQL Server 2012。  
  
 如果安裝 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，則繼續分別使用 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，在一部電腦上裝載您的 MDS 資料庫。 但是，您必須升級 MDS 資料庫的結構描述，然後使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Web 應用程式來存取 MDS 資料庫。 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Web 應用程式無法再存取 MDS 資料庫。  
  
-   根據預設，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中，檔案會安裝到 *磁碟機*:\Program Files\Microsoft SQL Server\120\Master Data Services。  
  
-   根據預設，在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]中，檔案會安裝到 *磁碟機*:\Program Files\Microsoft SQL Server\110\Master Data Services。  
  
-   根據預設，在 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]中，檔案會安裝到 *磁碟機*:\Program Files\Microsoft SQL Server\Master Data Services。  
  
 若要執行此工作，請完成下列步驟。  
  
1.  安裝 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 及您想要的其他任何功能。  
  
    1.  開啟 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安裝程式精靈。  
  
    2.  按一下左窗格中的 [安裝]****。  
  
    3.  按一下右窗格中的 [新增 SQL Server 獨立安裝或將功能加入至現有安裝]****。  
  
    4.  在 [功能選擇]**** 頁面上，選取 [[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]]**** 以及您想要安裝的其他任何功能。  
  
    5.  完成精靈。  
  
2.  在安裝完成後，升級 MDS 資料庫結構描述。  
  
    1.  開啟 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版的 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]。  
  
        > [!IMPORTANT]  
        >  若要升級 MDS 資料庫結構描述，您必須以建立 MDS 資料庫時指定之系統管理員帳戶的身分登入。 在 MDS 資料庫的 mdm.tblUser 中，這位使用者的 [識別碼]**** 值為 **1**。 如需變更此使用者的詳細資訊，請參閱[將系統管理員帳戶變更 &#40;Master Data Services&#41;](../../master-data-services/change-the-system-administrator-account-master-data-services.md)。  
  
    2.  按一下左窗格中的 [資料庫組態]****。  
  
    3.  在右窗格中，按一下 [**選取資料庫**]，然後在另[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]一[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]部電腦上指定或資料庫實例的[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]資訊[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] （如果或已安裝在另一部電腦上）。  
  
    4.  按一下 [升級資料庫]**** 可啟動 [升級資料庫精靈]****。 如需詳細資訊，請參閱[升級資料庫精靈 &#40;Master Data Services 組態管理員&#41;](../../master-data-services/upgrade-database-wizard-master-data-services-configuration-manager.md)。  
  
3.  升級完成後，請建立 SQL Server 2014 Web 應用程式。  
  
    1.  開啟 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版的 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]。  
  
    2.  按一下左窗格中的 **[Web 組態]**。  
  
    3.  從右窗格的 [網站]**** 清單中，選取下列其中一個選項：  
  
        -   [預設的網站]****，然後按一下 [建立應用程式]****。  
  
        -   [建立新的網站]****。 建立網站時，便會自動建立新的 Web 應用程式。  
  
        > [!IMPORTANT]  
        >  在 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 版的 Master Data Services 組態管理員中，可讓您選取您在舊版 SQL Server ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 或 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]) 中的現有 MDS Web 應用程式。 您絕不能選取現有的 Web 應用程式，而是必須建立 MDS 的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Web 應用程式。 否則，當您嘗試將 Web 應用程式與升級的 MDS 資料庫建立關聯時，將會收到錯誤，說明因為該頁面的相關組態資料無效，所以無法存取所要求的頁面。  
        >   
        >  如果您要為 MDS Web 應用程式使用相同的名稱 (別名) 做為現有 ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) Web 應用程式，您必須先將 Web 應用程式和相關聯的應用程式集區從 IIS 刪除，然後使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版的 Master Data Services 組態管理員，以相同的名稱建立 Web 應用程式。 如需從 IIS 移除 Web 應用程式和應用程式集區的資訊，請參閱 [移除應用程式 (IIS)](https://go.microsoft.com/fwlink/?LinkId=323537) 和 [移除應用程式集區 (IIS)](https://go.microsoft.com/fwlink/?LinkId=323538)。  
  
4.  現在將此 Web 應用程式與升級的 MDS 資料庫產生關聯。  
  
    1.  在 [建立應用程式與資料庫間的關聯]**** 區段中，按一下 [選取]****。  
  
    2.  選取 MDS 資料庫。  
  
    3.  按一下 [套用]  。  
  
##  <a name="upgrade-with-restoring-a-database-from-backup"></a><a name="restore"></a> 包含從備份中還原資料庫的升級  
 在這種情況中，[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 會隨著 SQL Server 2008 R2 或 SQL Server 2012 安裝在同一部電腦或兩部不同的電腦上。 此外，資料庫會在升級之前，備份至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CTP2 之前的版本上，而且資料庫必須還原。  
  
-   根據預設，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中，檔案會安裝到 *磁碟機*:\Program Files\Microsoft SQL Server\120\Master Data Services。  
  
-   根據預設，在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]中，檔案會安裝到 *磁碟機*:\Program Files\Microsoft SQL Server\110\Master Data Services。  
  
-   根據預設，在 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]中，檔案會安裝到 *磁碟機*:\Program Files\Microsoft SQL Server\Master Data Services。  
  
 若要執行此工作，請完成下列步驟。  
  
1.  安裝 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 及您想要的其他任何功能。  
  
    1.  開啟 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安裝程式精靈。  
  
    2.  按一下左窗格中的 [安裝]****。  
  
    3.  按一下右窗格中的 [新增 SQL Server 獨立安裝或將功能加入至現有安裝]****。  
  
    4.  在 [功能選擇]**** 頁面上，選取 [[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]]**** 以及您想要安裝的其他任何功能。  
  
    5.  完成精靈。  
  
2.  還原備份的資料庫。  
  
3.  在安裝完成後，升級 MDS 資料庫結構描述。  
  
    1.  開啟 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版的 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]。  
  
        > [!IMPORTANT]  
        >  若要升級 MDS 資料庫結構描述，您必須以建立 MDS 資料庫時指定之系統管理員帳戶的身分登入。 在 MDS 資料庫的 mdm.tblUser 中，這位使用者的 [識別碼]**** 值為 **1**。 如需變更此使用者的詳細資訊，請參閱[將系統管理員帳戶變更 &#40;Master Data Services&#41;](../../master-data-services/change-the-system-administrator-account-master-data-services.md)。  
  
    2.  按一下左窗格中的 [資料庫組態]****。  
  
    3.  在右窗格中，按一下 [**選取資料庫**]，然後指定[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]或[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]資料庫實例的資訊。  
  
    4.  按一下 [升級資料庫]**** 可啟動 [升級資料庫精靈]****。 如需詳細資訊，請參閱[升級資料庫精靈 &#40;Master Data Services 組態管理員&#41;](../../master-data-services/upgrade-database-wizard-master-data-services-configuration-manager.md)。  
  
4.  升級完成後，請建立 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Web 應用程式。  
  
    1.  開啟 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版的 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]。  
  
    2.  按一下左窗格中的 **[Web 組態]**。  
  
    3.  從右窗格的 [網站]**** 清單中，選取下列其中一個選項：  
  
        -   [預設的網站]****，然後按一下 [建立應用程式]****。  
  
        -   [建立新的網站]****。 建立網站時，便會自動建立新的 Web 應用程式。  
  
        > [!IMPORTANT]  
        >  在 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 版的 Master Data Services 組態管理員中，可讓您選取您在舊版 SQL Server ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 或 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]) 中的現有 MDS Web 應用程式。 您絕不能選取現有的 Web 應用程式，而是必須建立 MDS 的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Web 應用程式。 否則，當您嘗試將 Web 應用程式與升級的 MDS 資料庫建立關聯時，將會收到錯誤，說明因為該頁面的相關組態資料無效，所以無法存取所要求的頁面。  
        >   
        >  如果您要為 MDS Web 應用程式使用相同的名稱 (別名) 做為現有 ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) Web 應用程式，您必須先將 Web 應用程式和相關聯的應用程式集區從 IIS 刪除，然後使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版的 Master Data Services 組態管理員，以相同的名稱建立 Web 應用程式。 如需從 IIS 移除 Web 應用程式和應用程式集區的資訊，請參閱 [移除應用程式 (IIS)](https://go.microsoft.com/fwlink/?LinkId=323537) 和 [移除應用程式集區 (IIS)](https://go.microsoft.com/fwlink/?LinkId=323538)。  
  
5.  現在將新的 Web 應用程式與升級的 MDS 資料庫建立關聯。  
  
    1.  在 [建立應用程式與資料庫間的關聯]**** 區段中，按一下 [選取]****。  
  
    2.  選取 MDS 資料庫。  
  
    3.  按一下 [套用]  。  
  
## <a name="troubleshooting"></a>疑難排解  
 **問題：** 當您開啟[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]或[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] web 應用程式時，會顯示「用戶端版本與資料庫版本不相容」錯誤訊息。  
  
 **解決方案：** 當[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]或[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]主資料管理員 web 應用程式嘗試存取已升級為[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Master Data Services 的資料庫時，就會發生這個問題。 您必須改用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Web 應用程式。  
  
 如果您升級 MDS 資料庫結構描述時，未在 IIS 中停止 [MDS 應用程式集區]**** 然後再重新啟動，也可能會發生此問題。 重新啟動 [MDS 應用程式集區]**** 即可更正此問題。  
  
## <a name="see-also"></a>另請參閱  
 [安裝 Master Data Services](../../master-data-services/install-windows/install-master-data-services.md)  
  
  
