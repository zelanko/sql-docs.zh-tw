---
title: "設定處理選項 (SharePoint 整合模式的 Reporting Services) |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SharePoint integration [Reporting Services], content management
- snapshots [Reporting Services], creating
ms.assetid: 453b19a1-739a-4b67-aeea-2069b52204e1
caps.latest.revision: 15
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8f2a5c52f4fa9b04026490c1e66243bf0d660c13
ms.contentlocale: zh-tw
ms.lasthandoff: 06/13/2017

---
# <a name="set-processing-options-reporting-services-in-sharepoint-integrated-mode"></a>設定處理選項 (SharePoint 整合模式的 Reporting Services)
  您可以對 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表設定處理選項，以指定資料開始處理的時間。 您還可以設定報表處理的逾時值，以及決定是否要啟用目前報表之報表記錄的選項。  
  
-   您可以將報表以報表快照集的形式執行，以避免在任意時間 (例如，在排程備份期間) 執行報表。 報表快照集一般會按照排程建立和後續重新整理，讓您可以設定報表以及資料處理進行的正確時間。 如果報表所依據的，是要花很長時間執行的查詢，或者使用您希望在幾個小時內沒有人能存取之資料來源中之資料的查詢，您應將報表當成快照集執行。  
  
-   報表伺服器可以快取已處理報表的副本，並在使用者開啟報表時還原該副本。 快取是一種效能增強技術。 如果報表很大或存取頻繁，快取就可以縮短擷取報表所需的時間。  
  
-   報表記錄是之前所執行之報表副本的集合。 您可以使用報表記錄，以維護報表經過一段時間的記錄。 報表記錄不適用於包含機密或個人資料的報表。 因此，報表記錄只能包括使用一組認證 (預存認證或用於自動執行報表的認證) 來查詢資料來源的報表，此種認證是所有執行報表的使用者皆可使用的。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 使用 SharePoint 的簽出和簽入內容管理功能來儲存 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 內容類型的更新。 這包括建立報表快照集。 因此，如果您已經在文件庫上啟用版本控制，您將看到新報表記錄快照集建立時更新的報表版本。 這是更新快照集的副作用。 當快照集更新時，它會使報表的 LastExecution 屬性變更，因此造成報表版本變更。  
  
-   您可以指定逾時值，以便設定系統資源的使用限制。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint mode|  
  
 **本主題內容：**  
  
-   [設定資料重新整理選項](#bkmk_set_data_refresh)  
  
-   [設定報表快取選項](#bkmk_set_report_caching)  
  
-   [設定處理逾時值](#bkmk_set_processing)  
  
-   [設定報表記錄選項和限制](#bkmk_set_report_history)  
  
-   [設定資料庫逾時](#bkmk_set_database_timeout)  
  
##  <a name="bkmk_set_data_refresh"></a> 設定資料重新整理選項  
  
1.  指向程式庫中的報表。  
  
2.  按一下向下箭頭，然後選取 **[管理處理選項]**。  
  
3.  在 **[資料重新整理選項]**中，按一下 **[使用快照集資料]**。 如果您看見「此報表不可從快照集執行，因為有一或多個資料來源認證未儲存。」，表示報告未設定為自動執行，而且您必須先修改資料來源以使用儲存的認證，才能設定此選項。  
  
4.  在 **[資料快照集選項]**中，選取 **[排程資料處理]**。  
  
5.  如果要使用現有的共用排程，請選取 **[在共用排程上]** ，否則，請按一下 **[在自訂排程上]**，然後按一下 **[設定]**。  
  
6.  選取頻率、排程，以及開始和結束日期，然後按一下 **[確定]**。  
  
7.  如果要立即建立搭配報表使用的快照集資料，而不想等到排程的資料處理發生，請在 **[資料快照集選項]**中選取 **[儲存此頁面時建立或更新快照集]** 。  
  
##  <a name="bkmk_set_report_caching"></a> 設定報表快取選項  
  
1.  指向程式庫中的報表。  
  
2.  按一下向下箭頭，然後選取 **[管理處理選項]**。  
  
3.  在 **[資料重新整理選項]**中，按一下 **[使用快取的資料]**。 如果您看見「無法快取此報表，因為有一或多個資料來源認證未儲存。」，表示報告未設定為自動執行，而且您必須先修改資料來源以使用儲存的認證，才能設定此選項。  
  
4.  在 **[快取選項]**中，指定快取過期的方式：  
  
    -   輸入分鐘數，快取將在經過此分鐘數之後過期。  
  
    -   使用共用排程按照排程中指定的時間清除快取。  
  
    -   建立自訂排程按照指定的時間清除快取。  
  
##  <a name="bkmk_set_processing"></a> 設定處理逾時值  
  
1.  指向程式庫中的報表。  
  
2.  按一下向下箭頭，然後選取 **[管理處理選項]**。  
  
3.  如果您要使用在報表伺服器層級指定的值，請在 [處理逾時] 中選取 [使用站台預設值]。 否則，請選取 [報表處理不會逾時] 或 [限制報表處理的秒數]，使用無逾時或其他逾時值覆寫該值。  
  
##  <a name="bkmk_set_report_history"></a> 設定報表記錄選項和限制  
  
1.  指向程式庫中的報表。  
  
2.  按一下向下箭頭，然後選取 **[管理處理選項]**。  
  
3.  在 **[記錄快照集選項]**中，指定資料處理發生和儲存的方式及時間。  
  
4.  如果要使用在報表伺服器層級指定的值，請在 **[記錄快照集限制]**中選取 **[使用站台預設值]** 。 否則，請選取 **[不限制快照集數目]** 或 **[限制快照集數目為]** 指定自訂值。  
  
##  <a name="bkmk_set_database_timeout"></a> 設定資料庫逾時  
  
1.  使用 Windows PowerShell 設定的 SharePoint 報表伺服器資料庫逾時。 如需詳細資訊，請參閱＜ [PowerShell cmdlets for Reporting Services SharePoint Mode](../../reporting-services/report-server-sharepoint/powershell-cmdlets-for-reporting-services-sharepoint-mode.md)＞的＜取得並設定 Reporting Services 應用程式資料庫的屬性＞一節。  
  
## <a name="see-also"></a>請參閱＜  
 [設定報表處理屬性](../../reporting-services/report-server/set-report-processing-properties.md)   
 [快取報表 &#40;SSRS&#41;](../../reporting-services/report-server/caching-reports-ssrs.md)   
 [設定報表和共用資料集處理的逾時值 &#40;SSRS&#41;](../../reporting-services/report-server/setting-time-out-values-for-report-and-shared-dataset-processing-ssrs.md)  
  
  
