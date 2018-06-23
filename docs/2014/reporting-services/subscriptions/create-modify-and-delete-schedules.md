---
title: 建立、修改和刪除共用排程 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- report-specific schedules [Reporting Services]
- shared schedules [Reporting Services]
- modifying schedules
- removing schedules
- shared schedules [Reporting Services], creating
- shared schedules [Reporting Services], modifying
- schedules [Reporting Services], deleting
- deleting schedules
- schedules [Reporting Services], creating
- schedules [Reporting Services], modifying
- shared schedules [Reporting Services], deleting
ms.assetid: 05da5f3d-9222-43a9-893b-aa10f0f690f8
caps.latest.revision: 45
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: c4ac89d35cfe118cb82e945ef48d87c24b56abed
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031373"
---
# <a name="create-modify-and-delete-schedules"></a>Create, Modify, and Delete Schedules
  使用本主題可讓您了解如何建立、修改和刪除排程。  
  
 本主題內容：  
  
-   [共用排程的管理概觀](#bkmk_overview)  
  
-   [建立及管理共用的排程 （SharePoint 模式）](#bkmk_sharepoint)  
  
-   [建立及管理共用的排程 （原生模式）](#bkmk_native)  
  
##  <a name="bkmk_overview"></a> 共用排程的管理概觀  
 若要管理原生模式的共用的排程，請使用報表管理員中的 [排程] 頁面或 [共用排程] 資料夾中的[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。 如果是 SharePoint 模式，請使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式的管理頁面。  
  
 您可以檢視所有為報表伺服器定義的共用排程、暫停與繼續排程 (只能在報表管理員上進行)，以及選取要修改或刪除的排程。 [共用排程] 頁面中會有每一個排程狀態的下列摘要資訊：頻率、擁有者、到期日與狀態。  
  
 您可以透過下列方式來區別某個共用排程是否使用中：  
  
-   在 [共用排程] 頁面上檢查 [上次執行] 日期、[下次執行] 日期以及 [狀態] 欄位中的值。 若因為排程已過期而不再執行，到期日就會顯示在 [狀態] 欄位中。  
  
-   檢視給定之共用排程的 [報表] 頁面。 此頁面會列出使用共用排程的所有報表和共用資料集。  
  
-   檢視報表執行記錄檔或追蹤記錄，以便判斷報表是否已在排程指定的時間執行。 如需詳細資訊，請參閱 [Reporting Services 記錄檔和來源](../report-server/reporting-services-log-files-and-sources.md)。  
  
##  <a name="bkmk_sharepoint"></a> 建立及管理共用排程 (SharePoint 模式)  
 共用排程是一種多用途排程，可提供現成的排程資訊給任何數目的報表或訂閱。 您可以只建立共用排程一次，然後等到需要排程資訊時，在訂閱或屬性頁面中參考它。 共用排程可以集中管理、暫停和繼續。 相對地，您必須手動編輯自訂排程，才能避免執行報表或訂閱。  
  
 您必須具有網站管理員的身分，才能在 SharePoint 網站上建立、修改或刪除共用排程。  
  
 您可以依排程的描述性名稱來識別特定的排程。 如果沒有指定名稱，便會根據排程的相關事實 (例如排程的循環模式或執行日期和時間) 來建立預設名稱。  
  
> [!NOTE]  
>  建立共用排程需要 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務。  
  
### <a name="create-shared-schedules-sharepoint"></a>建立共用排程 (SharePoint)  
  
##### <a name="to-create-shared-schedules"></a>若要建立共用排程  
  
1.  按一下 **[網站動作]**。  
  
2.  按一下 **[站台設定]**。  
  
3.  在 [Reporting Services] 區段中，按一下 **[管理共用排程]**。  
  
4.  按一下 **[加入排程]** ，開啟 [排程屬性] 頁面。  
  
5.  輸入排程的描述性名稱。 在用來處理 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表的應用程式頁面上，這個名稱會出現在整個網站中排程定義頁面的下拉清單方塊中。 避免使用難讀的冗長名稱。 務必按照命名慣例，在名稱開頭放入最多描述資訊。  
  
6.  選擇頻率。 依據您所選擇的頻率而定，出現在頁面上的排程選項可能會改變以支援該頻率 (例如，如果您選擇 [月]，各月份的名稱將會出現在頁面上)。  
  
7.  定義排程。 單一排程無法支援所有的排程組合。  
  
8.  設定開始和結束日期。  
  
9. 按一下 [確定] 。  
  
### <a name="delete-shared-schedules-sharepoint"></a>刪除共用排程 (SharePoint)  
 無論是共用或報表特定排程，所有排程都必須手動刪除。 如果您刪除使用中的共用排程，該排程的所有參考都會取代成非特定的自訂排程 (亦即沒有日期或時間資訊的自訂排程)。  
  
 刪除排程與造成它過期是不相同的。 到期日是用來停止排程，但不會刪除它。 因為排程是用來自動化報表伺服器作業，所以永遠不會自動刪除。 過期的排程會提供證據給報表伺服器管理員，以說明自動化處理序突然停止的原因。 如果沒有顯示過期排程，報表伺服器管理員可能會誤判問題，或浪費不必要的時間嘗試解決功能正常的處理序。  
  
 已經過期的自訂排程會繼續附加至報表。 您可以檢查排程的結束日期，判斷它是否過期。 過期的共用排程會保留在 [共用排程] 清單中。 [狀態] 欄位會指示排程是否已過期。 您可以延長結束日期來恢復排程，或者，若您不再需要排程參考時，可以移除它。  
  
##### <a name="to-delete-a-shared-schedule"></a>若要刪除共用排程  
  
1.  按一下 **[網站動作]**。  
  
2.  按一下 **[站台設定]**。  
  
3.  在 [Reporting Services] 區段中，按一下 **[管理共用排程]**。  
  
4.  選取排程，然後按一下 **[刪除]**。  
  
##  <a name="bkmk_native"></a> 建立及管理共用的排程 （原生模式）  
 您必須使用報表管理員中的 [排程] 頁面或 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中的 [共用排程] 資料夾，手動刪除共用排程。 如果您刪除使用中的共用排程，所有的參考都會以報表特定排程取代。  
  
 當您刪除報表或訂閱，或者選擇不同的方法來執行報表或訂閱時，系統就會刪除報表和訂閱特有的排程。 例如，選擇 [永遠以最新的資料執行此報表] 將會刪除您建立為以報表執行快照集的方式執行報表的報表特有排程。  
  
 刪除排程與造成它過期是不相同的。 到期日是用來停止排程，但不會刪除它。 因為排程是用來自動化大量功能，所以永遠不會自動刪除。 過期的排程會提供證據給報表伺服器管理員，以說明自動化處理序突然停止的原因。 如果沒有顯示過期排程，報表伺服器管理員就會誤判問題，或花不必要的時間嘗試解決功能正常的處理序。  
  
 已經過期的報表特定排程會繼續附加至報表。 您可以檢查排程的結束日期，判斷它是否過期。 過期的共用排程會保留在 [共用排程] 清單中。 [狀態] 欄位會指示排程是否已過期。 您可以延長結束日期來恢復排程，或者，若您不再需要排程參考時，可以移除它。  
  
### <a name="create-delete-or-modify-a-shared-schedule-report-manager"></a>建立、刪除或修改共用排程 (報表管理員)  
 建立與修改排程，包含決定排程何時執行的設定頻率選項。  
  
-   共用排程會建立為個別項目。 建立之後，您可以在定義訂閱或其他已排程的作業時參考它們。  
  
-   報表特定排程是當您定義訂閱或設定報表執行屬性時建立的；填寫排程資訊是定義訂閱或設定屬性的一部分。 若要定義報表特定排程，請您開啟使用它的報表或訂閱。  
  
 共用排程包含在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器上執行之任何已發行報表和訂閱數目可用的排程與循環資訊。 如果您擁有許多同時執行的報表和訂閱，就可以針對這些作業建立共用排程。 如果您之後想要變更循環模式或結束日期，可以在單一位置進行變更。  
  
 共用排程的維護方式比較簡單，而且在管理排程作業方面提供更大的彈性。 例如，您可以暫停並繼續共用排程。 此外，如果您發現同時執行的排程作業過多，就可以建立在不同時間執行的多個共用排程，然後調整排程資訊，直到處理負載平均分散到報表伺服器為止。  
  
 您可以在任何時候建立或修改排程。 不過，如果排程在您修改完成之前便開始執行，則會使用舊版排程。 修訂的排程在您儲存之前不會生效。  
  
 如果您修改共用排程，就可以在進行變更之前暫停它。 當您繼續排程時，變更便會生效。  
  
##### <a name="to-create-or-modify-a-shared-schedule-report-manager"></a>若要建立或修改共用排程 (報表管理員)  
  
1.  啟動[報表管理員 &#40;SSRS 原生模式&#41;](../report-manager-ssrs-native-mode.md)。  
  
2.  在報表管理員中，按一下全域工具列上的 [網站設定] **[站台設定]**。  
  
3.  按一下 **[排程]**。  
  
4.  按一下 **[新增排程]**。 若要修改現有的排程，請按一下排程的名稱。  
  
5.  輸入排程的描述性名稱。  
  
6.  選取 **[小時]**、 **[天]**、 **[週]** 或 **[月]**。 按 **[一次]** ，即可建立只執行一次的排程。 當您指定排程的基礎時，其他選項會出現。  
  
7.  選擇性地選取排程的開始日期。 預設值是目前的日期。 您也可以選擇較晚的日期，來延後排程的開始時間。  
  
8.  選擇性地選取結束排程的日期。 排程會在此日期停止執行，但不會遭到刪除。  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##### <a name="to-delete-a-shared-schedule-report-manager"></a>若要刪除共用排程 (報表管理員)  
  
1.  在報表管理員中，按一下全域工具列上的 [網站設定] **[站台設定]**。  
  
    > [!NOTE]  
    >  如果**站台設定**是無法使用，您沒有存取站台設定的權限。  
  
2.  在頁面上的 **[其他]** 區段中，按一下 **[管理共用排程]**。  
  
3.  選取要刪除之排程旁邊的核取方塊，然後按一下 **[刪除]**。  
  
 如果您刪除了多個報表和訂閱所使用的共用排程，報表伺服器將會針對先前使用此共用排程的每個報表和訂閱建立個別的排程。 每個新的個別排程將包含共用排程中原本指定的日期、時間和循環模式。 請注意， [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 不會提供個別排程的集中管理功能。 如果您刪除了共用排程，現在就必須針對每個個別項目維護排程資訊。  
  
 如果您不確定是否使用了共用排程，請考慮改在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中刪除它。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 提供的共用排程管理功能與報表管理員相同，但是它會提供額外的 [報表] 頁面，其中顯示每個使用此排程之報表的名稱。  
  
### <a name="create-delete-or-modify-a-shared-schedule-management-studio"></a>建立、刪除或修改共用排程 (Management Studio)  
 共用排程包含在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器上執行之任何已發行報表和訂閱數目可用的排程與循環資訊。 如果您擁有許多同時執行的報表和訂閱，就可以針對這些作業建立共用排程。 如果您之後想要變更循環模式或結束日期，可以在單一位置進行變更。  
  
 共用排程的維護方式比較簡單，而且在管理排程作業方面提供更大的彈性。 例如，您可以暫停並繼續共用排程。 此外，如果您發現同時執行的排程作業過多，就可以建立在不同時間執行的多個共用排程，然後調整排程資訊，直到處理負載平均分散到報表伺服器為止。  
  
##### <a name="to-create-or-modify-a-shared-schedule-management-studio"></a>若要建立或修改共用排程 (Management Studio)  
  
1.  啟動 SQL Server Management Studio 並連接至報表伺服器執行個體。  
  
2.  在 [物件總管] 中，展開報表伺服器節點。  
  
3.  共用排程] 資料夾中，以滑鼠右鍵按一下，然後按一下 [**新排程**。 就會顯示 **[新增共用排程]** 對話方塊的 [一般] 頁面。  
  
     若要修改現有的共用排程，請展開 [共用排程] 資料夾、以滑鼠右鍵按一下您要修改的排程，然後按一下 [屬性]。  
  
4.  輸入排程的描述性名稱。  
  
5.  選擇性地選取排程的開始日期。 預設值是目前的日期。  
  
6.  選擇性地選取排程的結束日期。 排程會在此日期停止執行，但不會遭到刪除。  
  
7.  若要設定重複執行排程，請選取 **[小時]**、 **[天]**、 **[週]** 或 **[月]**。 就會顯示其他選項。 請根據您偏好的小時、天、週或月，使用這些選項來設定排程頻率。  
  
     若要指定單次 (非重複執行) 排程，請選取 [一次]，然後指定 [開始時間]。  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##### <a name="to-delete-a-shared-schedule-management-studio"></a>若要刪除共用排程 (Management Studio)  
  
1.  在 [物件總管] 中，展開報表伺服器節點。  
  
2.  展開 [共用排程] 資料夾，以滑鼠右鍵按一下您要刪除的排程，然後按一下 [刪除]。 **[刪除目錄項目]** 對話方塊隨即顯示。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 如果您刪除了多個報表和訂閱所使用的共用排程，報表伺服器將會針對先前使用此共用排程的每個報表和訂閱建立個別的排程。 每個新的個別排程將包含共用排程中原本指定的日期、時間和循環模式。 請注意， [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 不會提供個別排程的集中管理功能。 如果您刪除了共用排程，現在就必須針對每個個別項目維護排程資訊。 刪除共用的排程之前，請先使用[報表頁面](../tools/schedule-properties-reports-page.md)來判斷哪些報表目前正在使用共用的排程。  
  
## <a name="see-also"></a>另請參閱  
 [[排程]](schedules.md)   
 [暫停及繼續共用排程](pause-and-resume-shared-schedules.md)   
 [快取報表 &#40;報表管理員&#41;](../report-server/cache-a-report-report-manager.md)   
 [將快照集新增至報表記錄 &#40;報表管理員&#41;](../report-server/add-a-snapshot-to-report-history-report-manager.md)  
  
  