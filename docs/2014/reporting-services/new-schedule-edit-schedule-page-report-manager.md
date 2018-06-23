---
title: 新的排程： 編輯排程頁面 （報表管理員） |Microsoft 文件
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 52a4d250-e185-4116-a29c-d809940a00fb
caps.latest.revision: 27
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 019cb1a12e25ac3c347d1dbdb72296c2f2a888f3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36033608"
---
# <a name="new-schedule-edit-schedule-page-report-manager"></a>新的排程： 編輯排程頁面 （報表管理員）
  使用 [新增排程 / 編輯排程] 頁面，即可建立報表的排程。 排程可用於訂閱、重新整理快取報表，以及建立將快照集建立成獨立項目，或建立在報表歷程記錄中。  
  
> [!NOTE]  
>  並非所有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]版本都提供此功能。 如需所支援的版本功能的清單[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，請參閱[支援的 SQL Server 2014 的版本功能](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
 您只能為可以自動執行的報表建立排程。 您必須將報表資料來源認證儲存在報表伺服器資料庫中，才能自動執行報表。 如需詳細資訊，請參閱[資料來源 屬性頁&#40;報表管理員&#41;](../../2014/reporting-services/data-sources-properties-page-report-manager.md)。  
  
 單一排程中無法支援所有的頻率組合。 例如，若要在每星期五下午 12:00 到下午 4:00。 就必須建立指定星期五為執行日期的兩個每日排程，一個開始時間為下午 12:00， 另一個開始時間為下午 4:00。  
  
 排程處理是以主控和處理排程之報表伺服器的本機時間為基礎。  
  
## <a name="navigation"></a>導覽  
 您可以使用下列程序，在使用者介面 (UI) 中導覽至這個位置。  
  
### <a name="to-open-the-new-schedule-or-edit-schedule-page-from-the-execution-properties-page-of-a-report"></a>若要從報表的執行屬性頁面開啟新增排程或編輯排程頁面  
  
1.  開啟報表管理員，然後找出您想要設定排程的報表。  
  
2.  將滑鼠停留在該報表上，然後按一下下拉箭號。  
  
3.  在下拉式功能表中，按一下 **[管理]**。 這樣就會開啟該模型的 [一般] 屬性頁面。  
  
4.  選取 **[執行]** 索引標籤。  
  
5.  選取 **[從報表執行快照集轉譯此報表]** 選項。 接著，選取 **[使用下列排程將快照集加入至報表記錄]** 並選取 **[報表特定排程]**。 然後，按一下 **[設定]**。  
  
### <a name="to-open-the-new-schedule-or-edit-schedule-page-from-the-history-properties-page-of-a-report"></a>若要從報表的記錄屬性頁面開啟新增排程或編輯排程頁面  
  
1.  開啟報表管理員，然後找出您想要設定排程的報表。  
  
2.  將滑鼠停留在該報表上，然後按一下下拉箭號。  
  
3.  在下拉式功能表中，按一下 **[管理]**。 這樣就會開啟該模型的 [一般] 屬性頁面。  
  
4.  選取 **[記錄]** 索引標籤。  
  
5.  選取 **[使用下列排程將快照集加入至報表記錄]** 並選取 **[報表特定排程]**。 然後，按一下 **[設定]**。  
  
### <a name="to-open-the-new-schedule-or-edit-schedule-page-from-the-subscriptions-page"></a>若要從訂閱頁面開啟新增排程或編輯排程頁面  
  
1.  開啟報表管理員，然後找出您想要設定排程的報表。  
  
2.  將滑鼠停留在該報表上，然後按一下下拉箭號。  
  
3.  在下拉式功能表中，  
  
    -   按一下 **[管理]**。 這樣就會開啟該報表的 [一般] 屬性頁面。 然後，選取 **[訂閱]** 索引標籤。  
  
    -   按一下 **[訂閱]**。 這樣就會開啟該報表的 **[訂閱]** 屬性頁面。  
  
4.  在工具列中，按一下 **[新增訂閱]** 或選取要編輯的現有訂閱。  
  
5.  在 **[訂閱處理選項]** 底下，按一下 **[新增排程]**。  
  
## <a name="options"></a>選項。  
 **排程詳細資料**  
 選取決定何時執行報表及其執行頻率的選項。 頻率選項有層次之分。 第一組選項指定頻率的類別 (每小時、每日、每週等)。 顯示的第二組選項是以您的初始選擇為基礎。  
  
-   **[小時]** 會定義以每小時間隔執行的排程。 使用 **[開始和結束日期]** 區段，即可指定要執行排程的日期。  
  
-   **[天]** 會定義在您所選取日子之特定時間執行的排程。 您可以下列方式指定日子： 每個\<*天*>、 每個工作天和每\<*數目*> 天。 選擇一種方式就會使其他方式失效，即使其他日子看似已經選取也一樣。  
  
-   **[週]** 會定義在每週間隔之特定時間執行的排程。 此間隔可以是整週 (例如每兩週) 或是其中的日期。  
  
-   **[月]** 會定義以每月為基礎執行的排程。 在月份中可以根據模式來選擇日期 (例如每月的最後一個星期日) 或特定的日期 (例如 1 和 15 表示每月的第一和第十五日)。 使用逗號和連字號，可以指定多天和範圍，例如 1、5、7-12、21。  
  
-   **[一次]** 會定義只執行一次的排程。 使用 **[開始和結束日期]** 區段，即可指定要執行排程的日期。 此排程在處理過後立即過期。  
  
 **開始和結束日期**  
 指定決定排程生效的開始日期，以及決定排程過期的結束日期。  
  
 不會通知排程過期。 在結束日期之後，就不會再執行排程。 不會刪除過期的排程。 只能手動刪除排程。 因此，如果選擇繼續執行排程，您可以延展其結束日期。  
  
## <a name="see-also"></a>另請參閱  
 [報表管理員&#40;SSRS 原生模式&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [建立、修改和刪除共用排程](subscriptions/create-modify-and-delete-schedules.md)   
 [報表管理員 F1 說明](../../2014/reporting-services/report-manager-f1-help.md)  
  
  