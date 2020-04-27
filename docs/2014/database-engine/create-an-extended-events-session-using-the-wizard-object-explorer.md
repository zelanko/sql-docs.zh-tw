---
title: 使用 Wizard 建立擴充事件會話（物件總管） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- Sql12.ssms.XeWizard.Summary.f1
- Sql12.ssms.XeWizard.SetSessionProperties.f1
- Sql12.ssms.XeWizard.CaptureAddFields.f1
- Sql12.ssms.XeWizard.SelectEvents.f1
- Sql12.ssms.XeWizard.SpecifySessionTargets.f1
- Sql12.ssms.XeWizard.Welcome.f1
- sql12.ssms.XeWizard.Welcome.f1
- Sql12.ssms.XeWizard.ChooseTemplate.f1
- Sql12.ssms.XeWizard.SetSessionEventFilters.f1
- Sql12.ssms.XeWizard.Results.f1
helpviewer_keywords:
- Sql11.ssms.XeWizard.CaptureAddFields.f1
- Sql11.ssms.XeWizard.SetSessionEventFilters.f1
- Sql11.ssms.XeWizard.SpecifySessionTargets.f1
- Sql11.ssms.XeWizard.Results.f1
- Sql11.ssms.XeWizard.ChooseTemplate.f1
- Sql11.ssms.XeWizard.SetSessionProperties.f1
- Sql11.ssms.XeWizard.Welcome.f1
- Sql11.ssms.XeWizard.Summary.f1
- Sql11.ssms.XeWizard.SelectEvents.f1
ms.assetid: 80c0456f-17c0-41d8-b2aa-502a2f3bb6de
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cdc50e81bcc58722a3c04fc8516b9158072533cf
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66065063"
---
# <a name="create-an-extended-events-session-using-the-wizard-object-explorer"></a>使用精靈建立擴充事件工作階段 (物件總管)
  為了幫助您選取及擷取伺服器上的事件，「擴充事件」包含了 [新增工作階段精靈]，可引導您建立「擴充事件」工作階段的步驟。 [新增工作階段精靈] 會公開大部分的擴充事件功能。 [新增工作階段對話方塊](../../2014/database-engine/create-an-extended-events-session-using-the-new-session-dialog.md)也讓您定義擷取、顯示及分析資料的擴充事件工作階段。 [新增工作階段] 對話方塊會公開所有擴充事件功能。  
  
### <a name="to-open-the-new-session-wizard"></a>若要開啟新增工作階段精靈  
  
1.  在 [物件總管] 中，依序展開 **[管理]** 節點和 **[擴充事件]**。  
  
2.  以滑鼠右鍵按一下 [工作階段]****，然後按一下 [新增工作階段精靈]****。  
  
### <a name="use-the-following-new-session-wizard-pages-to-create-an-event-session"></a>使用下列新增工作階段精靈頁面來建立事件工作階段  
  
-   [簡介](#BKMK_Welcome)  
  
-   [設定工作階段屬性](#BKMK_SetSessionProperties)  
  
-   [選擇範本](#BKMK_ChooseTemplate)  
  
-   [選取要擷取的事件](#BKMK_SelectEventsToCapture)  
  
-   [擷取全域欄位](#BKMK_CaptureGlobalFields)  
  
-   [設定工作階段事件篩選](#BKMK_SetSessionEventFilters)  
  
-   [指定工作階段資料存放區](#BKMK_SpecifySessionDataOutput)  
  
-   [摘要](#BKMK_Summary)  
  
-   [建立事件會話](#BKMK_CreateEventSession)  
  
##  <a name="introduction"></a><a name="BKMK_Welcome"></a>問世  
 在 [簡介]**** 頁面上，執行下列動作：  
  
-   在 [新增工作階段精靈] 的 [簡介]**** 頁面上，按 [下一步]****。  
  
     如果您將使用精靈一次以上，而且不想在每次啟動精靈時閱讀簡介，請選取 [不要再顯示此頁面]**** 核取方塊。  
  
##  <a name="set-session-properties"></a><a name="BKMK_SetSessionProperties"></a>設定會話屬性  
 在 [設定工作階段屬性]**** 頁面上，執行下列動作：  
  
-   在 [工作階段名稱]**** 方塊中，為事件工作階段輸入有意義的名稱。  
  
     如果當您啟動伺服器時想要啟動工作階段，請選取 [在伺服器啟動時啟動事件工作階段]**** 核取方塊，然後按 [下一步]****。  
  
##  <a name="choose-template"></a><a name="BKMK_ChooseTemplate"></a>選擇範本  
 在 [選擇範本]**** 頁面上，執行下列動作：  
  
-   選取 [使用此事件工作階段範本]**** 選項，從針對常見問題所設計的一組預先設定的範本中選取。 從下拉式清單中選取您想要使用的範本，然後按 [下一步]****。  
  
     -或-  
  
-   如果您不想要使用任何預先設定的範本，請選取 [不使用範本]**** 選項，然後按 [下一步]****。  
  
##  <a name="select-events-to-capture"></a><a name="BKMK_SelectEventsToCapture"></a>選取要捕獲的事件  
 在 [選取要擷取的事件]**** 頁面上，執行下列動作：  
  
1.  從 [事件程式庫]**** 選取您想要擷取的事件，然後按一下向右箭號。 您可以使用 Shift+按一下滑鼠左鍵或 Ctrl+按一下滑鼠左鍵，在 [事件程式庫] 中選取多個事件。  
  
     您可以從下拉式清單方塊中選取您想要搜尋事件的方式。 例如，您可以搜尋事件名稱或是事件名稱及其說明。 您可以在 [事件程式庫]**** 方塊中輸入您想要搜尋的文字，以搜尋資料表中的任何文字。 例如，如果您想要尋找**lock_acquired**事件，您可以輸入**lock**或**lock 取得**。  
  
     您所選取的事件會出現在 [選取的事件]**** 方塊中。 若要從 [選取的事件]**** 方塊中移除事件，請按一下向左箭號。  
  
2.  選取您想要擷取的事件之後，請按 [下一步]****。  
  
    > [!NOTE]  
    >  依預設，[偵錯]**** 通道的事件是隱藏的。 若要顯示偵錯事件，請從 [通道]**** 下拉式清單中選取 [偵錯]****。  
  
##  <a name="capture-global-fields"></a><a name="BKMK_CaptureGlobalFields"></a>捕捉全域欄位  
 您可以使用全域欄位 (也稱為動作)，將選定事件的單一個或多個動作產生關聯。 如果您在 [選擇範本]**** 頁面上選取範本，此範本中定義的所有全域欄位都會顯示在這個頁面上。  
  
 在 [擷取全域欄位]**** 頁面上，執行下列動作：  
  
-   選取您想要針對事件工作階段擷取的全域欄位，然後按 [下一步]****。  
  
     您可以選取或取消選取全域欄位旁邊的核取方塊，以移除或加入全域欄位。  
  
    > [!NOTE]  
    >  選取的動作會依 [名稱]**** 排序，好讓您依字母順序檢視關聯的動作。 您可以按一下欄位名稱旁邊的欄位標題，依說明或啟用/停用狀態來排序。  
  
##  <a name="set-session-event-filters"></a><a name="BKMK_SetSessionEventFilters"></a>設定會話事件篩選器  
 您可以套用篩選 (也稱為述詞) 來限制您想要擷取的事件。 在 [設定工作階段事件篩選]**** 頁面上，執行下列動作：  
  
1.  如果您不使用預先設定的範本，請建立您的篩選準則，然後按 [下一步]****。  
  
     如果您使用預先設定的範本，則在 [範本中的篩選 (唯讀)]**** 區段中，[新增工作階段精靈] 會列出已從範本建立的篩選。  
  
2.  在 [其他篩選]**** 區段中，您可以為事件工作階段設定其他篩選。  
  
     您所設定的篩選會套用到所有選取的事件。 [新增工作階段精靈] 不支援為每個事件設定篩選。  
  
    > [!NOTE]  
    >  當您為篩選設定群組子句時，儲存結果之後會從篩選中移除多餘的括號。 例如，如果您建立篩選群組 **Clause 1** 和 **Clause 2**，括弧將會出現在子句的周圍。 當您儲存篩選之後，將會移除多餘的括號。 移除括號並不會影響篩選邏輯。  
  
##  <a name="specify-session-data-storage"></a><a name="BKMK_SpecifySessionDataOutput"></a>指定會話資料存放區  
 您可使用 [指定工作階段資料存放區]**** 頁面，指定您要如何收集資料進行分析。 SQL Server 擴充事件會使用資料輸出的目標。 目標會儲存事件資料，而且可以執行動作，例如寫入檔案及彙總事件資料。 在 [指定工作階段資料存放區]**** 頁面上，決定您要如何收集資料進行分析，然後執行下列動作：  
  
1.  如果是大型資料集而且要建立歷程記錄，請選取 [將資料儲存至檔案以供日後分析]**** 核取方塊，然後執行下列動作：  
  
    1.  在 [伺服器上的檔案名稱]**** 方塊中，輸入路徑和檔案名稱，或是按一下 [瀏覽]**** 指定伺服器上想要用來儲存資料的檔案目錄。  
  
    2.  在 [檔案大小上限]**** 方塊中，指定用於檔案目標的檔案大小上限。 如果未指定檔案大小上限，檔案可以成長到磁碟已滿。 預設檔案大小為 1 GB。  
  
    3.  選取 [啟用檔案換用]**** 核取方塊來啟用檔案目標的檔案換用。  
  
    4.  在 [檔案數量上限]**** 方塊中，指定您想要在檔案系統中保留的檔案數目上限。  
  
2.  如果要收集最近的資料，請選取 [只使用最新資料 (ring_buffer 目標)]**** 核取方塊，然後執行下列動作：  
  
    1.  在 [要保留的事件數目]**** 方塊中，使用向上和向下箭號來輸入或選取您想要保留的事件數目。  
  
    2.  在 [緩衝區記憶體大小上限]**** 方塊中，指定要使用的緩衝區記憶體最大數量。 當到達這個值時，將會捨棄現有的事件。  
  
    3.  如果您想要保留緩衝區中每一個類型的特定事件數目，請選取 [在緩衝區已滿時保留指定的事件數目 (每一類型)]**** 核取方塊。  
  
    4.  在 [要保留的事件數目 (每一類型)]**** 方塊中，使用向上和向下箭號來輸入或選取您想要保留的事件數目 (每一類型)。  
  
##  <a name="summary"></a><a name="BKMK_Summary"></a> 摘要  
 在 [摘要]**** 頁面上，執行下列動作：  
  
1.  請確定您的選擇正確無誤。 展開事件工作階段節點，以確認您的所有選擇都將包含在事件工作階段中。  
  
2.  按一下 [指令碼]****，將工作階段建立指令碼匯出到新的查詢編輯器視窗。  
  
3.  按一下 [完成]**** 建立事件工作階段。  
  
##  <a name="create-event-session"></a><a name="BKMK_CreateEventSession"></a>建立事件會話  
 在 [建立事件工作階段]**** 頁面上，於成功建立您的事件工作階段之後執行下列動作：  
  
1.  按一下 [在工作階段建立後立即啟動事件工作階段]**** 即可在關閉精靈之後啟動工作階段。 在您建立事件工作階段之後必須立即啟動此工作階段，才能監看即時資料。  
  
2.  按一下 [擷取同時監看畫面上的即時資料]****，檢視事件工作階段的即時資料。 建立工作階段之後，即時資料將會立即開始顯示追蹤。  
  
## <a name="see-also"></a>另請參閱  
 [使用新增工作階段對話方塊建立擴充事件工作階段](../../2014/database-engine/create-an-extended-events-session-using-the-new-session-dialog.md)  
  
  
