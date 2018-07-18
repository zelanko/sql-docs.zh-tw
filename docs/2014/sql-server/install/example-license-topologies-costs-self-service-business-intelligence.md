---
title: 授權拓撲和成本範例 SQL Server 2014 自助商業智慧 |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 682b8711-407a-48d1-9807-415d4c24dad6
caps.latest.revision: 13
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 4672647d8e9caae94e3b64fc43c3b687aa010920
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37185797"
---
# <a name="example-license-topologies-and-costs--for-sql-server-2014-self-service-business-intelligence"></a>SQL Server 2014 自助商業智慧的授權拓撲和成本範例
  本主題說明如何針對選取的高層級考量[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Business Intelligence 版或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Enterprise edition。 本主題包含數個內部部署 Microsoft 自助商業智慧 (BI) 拓撲的範例。 您可以利用這些範例所包含的版本和授權，在成本與效能之間取得最佳平衡。 本文提供的拓撲、伺服器數目和授權成本 **僅為範例**。 Microsoft [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 和 Microsoft SharePoint 2013 導入了幾項授權變更，提供更多的選項讓您選擇伺服器、使用者和裝置的授權方式。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 授權支援相同的商業智慧相關案例。  
  
-   
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 隨附於 Business Intelligence 版，它針對某些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本提供每個核心的授權方式。  
  
-   SharePoint 2013 針對外部網路與網際網路案例簡化了 SharePoint Server 的授權方式，以及簡化了 SharePoint Online 的選項。  
  
 購買之前，請瀏覽每項產品的「如何購買」(How to Buy) 區段，並連絡您的 Microsoft 業務代表或地區轉售商，洽詢有關您的特定授權需求的資訊。 如需最新授權計劃與成本的詳細資訊，請參閱以下主題：  
  
-   [關於授權 – SQL Server 2014](http://www.microsoft.com/licensing/about-licensing/sql2014.aspx)  
  
-   [SharePoint 2013 授權](http://office.microsoft.com/sharepoint/sharepoint-licensing-overview-collaboration-software-FX103789438.aspx)。  
  
 **本主題內容：**  
  
-   [SQL Server 商業智慧元件](#bkmk_bi_components)  
  
-   [SQL Server 2014 授權摘要](#bkmk_sql_server_license)  
  
-   [SharePoint 2013 授權摘要](#bkmk_sharepoint_license)  
  
-   [使用不同 PowerPivot 伺服器的 3 層拓撲](#bkmk_3tier_powerpivot)  
  
-   [3 層拓撲](#bkmk_3tier)  
  
-   [2 層拓撲](#bkmk_2tier)  
  
-   [參考與社群內容](#bkmk_reference)  
  
##  <a name="bkmk_bi_components"></a> SQL Server 商業智慧元件  
 本主題主要是要說明 SQL Server 和 SharePoint 伺服器技術。 本文中的成本與範例並未明確描述做為一個完整的用戶端和伺服器方案時您所需的 Microsoft Windows Server 或 Microsoft Office 元件。 本主題所涵蓋的 SQL Server 商業智慧元件是指在 SharePoint 模式中執行的 SQL Server Reporting Services 和 PowerPivot for SharePoint。 這些元件包含以下功能：  
  
-   瀏覽器中的互動式 PowerPivot 活頁簿。  
  
-   互動式[!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]SharePoint 中的報表。  
  
-   [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 圖庫、排程資料重新整理、管理儀表板。  
  
-   SharePoint 模式中的 Reporting Services，包括資料警示。  
  
 如需詳細資訊，請參閱中的功能資料表[安裝 SQL Server BI 功能來搭配 SharePoint &#40;PowerPivot 和 Reporting Services&#41;](../../../2014/sql-server/install/install-sql-server-bi-features-sharepoint-powerpivot-reporting-services.md)。  
  
## <a name="license-summary"></a>授權摘要  
 本節將摘要說明 SQL Server 和 SharePoint 的授權需求。 本資訊是高層級摘要資訊，只包含本文中用於拓撲圖表和成本範例中的案例。 如需更詳細的授權詳細資料，請檢閱本文所述的內容連結。 範例價格是以 Microsoft Open License 方案 (MOLP) 的價格為基礎。  
  
 常見的作法是針對執行 SQL Server Database Engine 的伺服器使用 **Enterprise 版** ，以及針對執行 Reporting Services 或 PowerPivot for SharePoint 的伺服器使用 **Business Intelligence 版** 。 不過，您的部署中的 **使用者數目** 和 **伺服器核心數目** 都會影響成本以及您對於要使用哪個版本的決定。  
  
###  <a name="bkmk_sql_server_license"></a> SQL Server 2014 授權摘要  
  
-   SQL Server Enterprise 版使用的是核心授權。 核心授權是以 **兩個核心** 為一套的方式出售。  
  
-   SQL Server BI 版本同時使用伺服器授權和用戶端存取授權 (CAL)。  
  
-   CAL 授權是以連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的每一個使用者或裝置來計算，而不論所連接的伺服器數目。  
  
-   核心授權則要求伺服器中的所有核心都由一個授權涵蓋。 伺服器中的每個實體處理器至少需要 **四** 個核心授權。  
  
 下表摘要說明用於部署設計和授權成本估計的授權詳細資料。 **注意：**  所顯示的價格僅為示範。  
  
|SQL Server 版本|SQL Server 授權 + 用戶端存取授權 (CAL)|SQL Server 核心授權|  
|-------------------------|---------------------------------------------------------|-----------------------------------|  
|Enterprise|不適用|**(是)** $6874 X [核心數目] X [核心因素]|  
|Business Intelligence|**(是)** $8592 + $199 (每個 CAL)|不適用|  
|Standard|**(Yes)**|**(Yes)**|  
  
 如需有關範例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]授權價格資訊，請參閱：  
  
-   [授權適用於虛擬環境](http://www.microsoft.com/licensing/about-licensing/virtualization.aspx)(http://www.microsoft.com/licensing/about-licensing/virtualization.aspx)。  
  
-   [SQL Server 2014 授權資料表-Microsoft 首頁](http://download.microsoft.com/download/6/6/F/66FF3259-1466-4BBA-A505-2E3DA5B2B1FA/SQL_Server_2014_Licensing_Datasheet.pdf)(http://download.microsoft.com/download/6/6/F/66FF3259-1466-4BBA-A505-2E3DA5B2B1FA/SQL_Server_2014_Licensing_Datasheet.pdf)。  
  
-   [SQL server 2014 版本與授權](http://www.microsoft.com/licensing/about-licensing/sql2014.aspx#tab=2)  
  
1.  **SQL Server 假設條件與詳細授權資訊：**  
  
2.  本主題中的圖表是使用 SQL Server 的 Enterprise 版做為資料庫伺服器，這樣就有一組完整的高可用性功能可供使用，例如，AlwaysOn 可用性群組。 如需詳細資訊，請參閱＜ [Features Supported by the Editions of SQL Server 2014](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)＞。  
  
3.  此範例中的伺服器全部都有 2 個 Intel Xeon 6 核心處理器，因此，在計算授權成本時， **SQL Server 核心因素** 就會是 **1** 。 如需有關核心因素和授權成本的詳細資訊，請參閱 < [SQL Server 核心因素資料表](http://download.microsoft.com/download/9/B/F/9BF63163-D8F9-4339-90AA-EBC9AAFC49AD/SQL2012_CoreFactorTable_Mar2012.pdf)(http://download.microsoft.com/download/0/C/8/0C85665B-11EA-4FF5-B37C-8CC21CF95AC4/BizTalk%202013_CoreFactorTable_**3.19.2013**。 v4.pdf)。  
  
###  <a name="bkmk_sharepoint_license"></a> SharePoint 2013 授權摘要  
 以下清單摘要說明用於部署設計和授權成本估計的授權模型。 所顯示的價格僅為示範。  
  
1.  Microsoft SharePoint Server 的每個執行個體都需要 SharePoint 伺服器授權。  
  
2.  若要計算 SharePoint Enterprise 授權，除了要為每個使用者或裝置分別購買一個 Microsoft SharePoint Server 2013 **Enterprise CAL 授權** 外，還要分別購買一個 Microsoft SharePoint Server 2013 **Standard CAL 授權**。  
  
3.  每個存取 SharePoint 伺服器的使用者或裝置都要購買一個 SharePoint CAL 授權。 您不需要為每一部伺服器購買 CAL 授權。  
  
 例如，如果您的環境是由 100 個使用者使用的 2 個執行個體所構成，則您的成本報價如下：  
  
-   Microsoft SharePoint Server 2013 Standard CAL license: <bpt id="p1">**</bpt>$107.99<ept id="p1">**</ept>  
  
-   Microsoft SharePoint Server 2013 Enterprise CAL license: <bpt id="p1">**</bpt>$94.99<ept id="p1">**</ept>  
  
-   Microsoft SharePoint Server 2013 license: <bpt id="p1">**</bpt>$6,412.99<ept id="p1">**</ept>  
  
 The cost would be: <bpt id="p1">**</bpt>$33,123.98<ept id="p1">**</ept>  
  
-   CAL 授權：($107.99 +$94.99) X 100) =$20,298.00  
  
-   伺服器授權：($6,412.99 X 2) =$12,825.98  
  
 **SharePoint 假設條件與詳細授權資訊：**  
  
 因為部署範例全部都是內部網路環境，因此需要 SharePoint CAL 授權。  
  
-   [SharePoint 完整授權清單](http://technet.microsoft.com/en-in/library/jj819267.aspx#bkmk_FeaturesOnPremise)(http://technet.microsoft.com/en-in/library/jj819267.aspx#bkmk_FeaturesOnPremise)。  
  
-   [如何購買 SharePoint](http://sharepoint.microsoft.com/en-in/Pages/buy.aspx) (http://sharepoint.microsoft.com/en-in/Pages/buy.aspx)。  
  
##  <a name="bkmk_3tier_powerpivot"></a> 3 層拓撲使用不同[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]伺服器  
 此範例將說明在 800 個或更少的使用者環境下，針對 SharePoint 應用程式伺服器和 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 伺服器來使用 SQL Server BI 版是成本最低的方案。 不過，如果有 800 個以上的使用者，SQL Server Enterprise 版的成本會比較低。 核心授權與使用者數目無關，因此當您比較核心和 CAL 授權成本以及使用者數目的增長時，就會有一個成本臨界點。 從臨界點向上推，Enterprise 版會是成本最低的方案。 若要判斷成本臨界值，請將需要購買授權的核心數目以及需要購買授權的使用者或裝置 CAL 數目所計算而得的成本做個比較。  
  
-   此範例是內部網路部署，因此需要為 SharePoint 2013 購買 SharePoint CAL 授權。  
  
-   應用程式角色 (2) 包括以 SharePoint 模式安裝的 SQL Server Reporting Services。  
  
     SharePoint 服務應用程式資料庫是在資料庫角色 (4) 伺服器上執行。  
  
-   在不同伺服器 (3) 上執行的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 2013 是 SharePoint 伺服器陣列外執行，可以安裝在伺服器上，不包含 SharePoint 安裝，改善效能。  
  
-   資料庫角色 (4) 會使用 SQL Server Enterprise，這樣就可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 AlwaysOn 可用性群組這個功能。  
  
 ![bi_license_3tiers_and_ASseparate](../../../2014/sql-server/install/media/bi-license-3tiers-and-asseparate.gif "bi_license_3tiers_and_ASseparate")  
  
 在 100 個使用者的環境中，SQL Server BI 版的成本會比較低。  
  
 ![bi_license_3tiers_and_ASseperate_calcs](../../../2014/sql-server/install/media/bi-license-3tiers-and-asseperate-calcs.gif "bi_license_3tiers_and_ASseperate_calcs")  
  
 不過，如果有 300 個使用者，則使用 SQL Server Enterprise 版的成本會比較低。  
  
 ![bi_license_3tiers_and_ASseperate_calcs2](../../../2014/sql-server/install/media/bi-license-3tiers-and-asseperate-calcs2.gif "bi_license_3tiers_and_ASseperate_calcs2")  
  
##  <a name="bkmk_3tier"></a> 3 層拓撲  
 此範例說明在 100 個或更少的使用者情況下，對於執行 SQL Server BI 功能的伺服器來說，使用 SQL BI 版的成本會比較低。 不過，如果有 500 個以上的使用者，SQL Server Enterprise 版的成本會比較低。  
  
-   此範例是內部網路部署，因此需要為 SharePoint 2013 購買 SharePoint CAL 授權。  
  
-   PowerPivot 模式 (2) 執行伺服器陣列外部的 analysis Services，但 PowerPivot 執行**相同的實體上**在另一個應用程式角色的伺服器。  
  
-   資料庫角色 (3) 會使用 SQL Server Enterprise 以便[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]功能，AlwaysOn 可用性群組。  
  
 ![bi_license_3tiers](../../../2014/sql-server/install/media/bi-license-3tiers.gif "bi_license_3tiers")  
  
 在 100 個使用者的環境中，SQL Server BI 版的成本會比較低。  
  
 ![bi_license_3tiers_calcs1](../../../2014/sql-server/install/media/bi-license-3tiers-calcs1.gif "bi_license_3tiers_calcs1")  
  
 不過，如果有 500 個使用者，則 SQL Server Enterprise 版的成本會比較低。  
  
 ![bi_license_3tiers_calcs3](../../../2014/sql-server/install/media/bi-license-3tiers-calcs3.gif "bi_license_3tiers_calcs3")  
  
##  <a name="bkmk_2tier"></a> 2 層拓撲  
 只有 2 層時，可使用 SQL Server Enterprise 版，這樣 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能 AlwaysOn 可用性群組就可供 SQL Server Database Engine 使用。 因此 SQL Server 版本之間沒有成本差異可比較。 唯一的變數是根據使用者數目計算的 SharePoint CAL 價格。  
  
-   此範例是內部網路部署，因此需要為 SharePoint 2013 購買 SharePoint CAL 授權。  
  
-   PowerPivot 模式中的 Analysis Services 是在伺服器陣列外執行，但 PowerPivot 是在做為 SQL Server Database Engine 的相同實體伺服器 (2) 上執行。  
  
 ![bi_license_2tiers](../../../2014/sql-server/install/media/bi-license-2tiers.gif "bi_license_2tiers")  
  
 ![bi_license_2tiers_calcs1](../../../2014/sql-server/install/media/bi-license-2tiers-calcs1.gif "bi_license_2tiers_calcs1")  
  
##  <a name="bkmk_reference"></a> 參考與社群內容  
  
### <a name="license-tools"></a>授權工具  
  
-   [Microsoft License Advisor](http://mla.microsoft.com/default.aspx) (http://mla.microsoft.com/default.aspx)。  
  
-   [用戶端存取授權 (CAL) 決定工具](http://www.microsoft.com/licensing/CalTool/)(http://www.microsoft.com/licensing/CalTool/)。  
  
-   [Microsoft Business Hub： 如何購買](http://www.microsoftbusinesshub.com/How_To_Buy#)(http://www.microsoftbusinesshub.com/How_To_Buy#)。  
  
### <a name="microsoft-license-information"></a>Microsoft 授權資訊  
  
-   [關於授權： 用戶端存取授權和管理授權](http://www.microsoft.com/licensing/about-licensing/client-access-license.aspx)(http://www.microsoft.com/licensing/about-licensing/client-access-license.aspx)。  
  
-   [關於授權： 的產品授權搜尋](http://www.microsoftvolumelicensing.com/default.aspx)(http://www.microsoftvolumelicensing.com/default.aspx)。  
  
-   [大量授權： 定價和購買方式](http://www.microsoft.com/licensing/how-to-buy/how-to-buy.aspx)(http://www.microsoft.com/licensing/how-to-buy/how-to-buy.aspx)。  
  
### <a name="community-content"></a>社群內容  
  
-   [SQL Server 2014 Developer Edition 授權](http://sqlmag.com/sql-server-2014/sql-server-2014-developer-edition-licensing)。  
  
-   [SQL Server 2014 授權變更](http://www.brentozar.com/archive/2014/04/sql-server-2014-licensing-changes)(http://www.brentozar.com/archive/2014/04/sql-server-2014-licensing-changes)。  
  
-   [SQL Server 2014 的授權變更](https://www.directionsonmicrosoft.com/sites/default/files/PDFs/Licensing_Changes_for_SQL_Server_2014.pdf)(https://www.directionsonmicrosoft.com/sites/default/files/PDFs/Licensing_Changes_for_SQL_Server_2014.pdf)。  
  
-   [評估授權成本的 SharePoint 2013](http://www.degdigital.com/blog/sharepoint-2013-licensing-for-dummies/) (http://www.degdigital.com/blog/sharepoint-2013-licensing-for-dummies/)。  
  
-   [Microsoft 大量授權客戶社群](http://www.microsoft.com/licensing/existing-customers/community.aspx)(http://www.microsoft.com/licensing/existing-customers/community.aspx)。  
  
  
