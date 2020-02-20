---
title: 將快照集新增至報表記錄 - Reporting Services | Microsoft Docs
ms.prod: reporting-services
ms.technology: reporting-services
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
ms.custom: ''
ms.date: 06/26/2019
ms.openlocfilehash: 2ada64f14c3564bd1e6c9846f890fdd8b287cb6f
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "68251933"
---
# <a name="add-a-snapshot-to-report-history"></a>將快照集加入至報表記錄

報表記錄是您在經過一段時間後建立之報表快照集的集合。 報表快照集是一種報表，它包含在特定時間點擷取的配置資訊和查詢結果。 報表快照集和視需要報表不同，視需要報表會在您選取報表時取得最新的查詢結果，而報表快照集是依排程處理，並儲存至報表伺服器。 您選取報表快照集以供檢視時，報表伺服器會從報表伺服器資料庫擷取儲存的報表，並顯示建立快照集當時的資料與配置。  
  
報表快照集不會以特定轉譯格式儲存。 而是只有在使用者或應用程式要求它時，報表快照集才以最後的檢視格式轉譯 (例如 HTML)。 延遲轉譯讓快照集具有可攜性。 報表可以使用要求的裝置或 Web 瀏覽器的正確格式轉譯。  
  
## <a name="to-manually-add-snapshots-to-report-history"></a>若要手動將快照集加入至報表記錄
  
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

1. 在報表管理員中，巡覽至 [內容]  頁面，將滑鼠游標停留在您想要檢視記錄的項目上方，然後按一下下拉箭號。
  
2. 在下拉式功能表中，按一下 **[檢視報表記錄]** 。  
  
3. 按一下 **[新增快照集]** 。 **[執行時]** 資料行裡會建立一個新的快照集。  
    > [!NOTE]
    > 若要啟用建立快照集功能，系統管理員必須將報表記錄設定為 [允許手動建立記錄]  。 如需詳細資訊，請參閱 [限制報表記錄 &#40;報表管理員&#41;](../reports/limit-report-history-report-manager.md)。

4. 按一下 [套用]  。
  
## <a name="to-automatically-add-all-snapshots-to-report-history"></a>若要自動將所有快照集加入報表記錄  
  
1. 若為已經設定成當做報表執行快照集執行的報表，您可以設定其他屬性，以便在每次重新整理快照集時，將快照集的副本儲存至報表記錄。  
  
2. 在報表管理員中，巡覽至 [內容]  頁面，將滑鼠游標停留在您想要檢視記錄的項目上方，然後按一下下拉箭號。  
  
3. 在下拉式功能表中，按一下 **[管理]** 。  
  
4. 按一下 **[快照集選項]** 。  
  
5. 選取 **[將所有報表執行快照集儲存在記錄中]** 的核取方塊。  
  
6. 按一下 [套用]  。  
  
## <a name="to-automatically-add-snapshots-to-report-history-based-on-a-schedule"></a>若要依照排程自動將快照集加入報表記錄  
  
1. 在報表管理員中，巡覽至 [內容]  頁面，將滑鼠游標停留在您想要檢視記錄的項目上方，然後按一下下拉箭號。  
  
2. 在下拉式功能表中，按一下 **[管理]** 。  
  
3. 按一下 **[快照集選項]** 。  
  
4. 選取 **[使用下列排程將快照集加入至報表記錄]** 的核取方塊。 執行下列其中一項：  
  
    - 選取 [報表特定排程]  。 填入排程詳細資料，選取排程的開始和結束日期，然後按一下 **[確定]** 。  

    - 選取 **[共用排程]** 。 從清單中，選取喜好的排程。  

5. 按一下 [套用]  。  
  
## <a name="see-also"></a>另請參閱

- [設定報表的執行屬性 &#40;報表管理員&#41;](../../reporting-services/reports/configure-execution-properties-for-a-report-report-manager.md)
- [限制報表記錄 &#40;報表管理員&#41;](../../reporting-services/reports/limit-report-history-report-manager.md)
- [排程](../../reporting-services/subscriptions/schedules.md)   
- [報表管理員 &#40;SSRS 原生模式&#41;](https://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)

::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"

## <a name="to-manually-add-snapshots-to-report-history"></a>若要手動將快照集加入至報表記錄
  
1. 在入口網站中，巡覽至您想要檢視其記錄的項目，並以滑鼠右鍵按一下該項目。  
  
2. 從下拉式功能表中選取 [管理]  。  
  
3. 選取 [記錄快照集]  索引標籤。  
  
4. 在 [記錄快照集]  頁面上，選取 [新增記錄快照集]  。 隨即建立新的快照集，並於下方的 [建立時間]  資料行中顯示目前日期和時間。  
  
    > [!NOTE]
    > 若要啟用建立快照集功能，系統管理員必須將報表記錄設定為 [允許手動建立記錄]  。 如需詳細資訊，請參閱[限制報表記錄 (入口網站)](../../reporting-services/reports/limit-report-history-report-manager.md)。

## <a name="to-add-snapshots-via-a-schedule-to-report-history"></a>透過排程將快照集新增至報表記錄

1. 在入口網站中，巡覽至您想要檢視其記錄的項目，並以滑鼠右鍵按一下該項目。  
  
2. 從下拉式功能表中選取 [管理]  。  
  
3. 選取 [記錄快照集]  索引標籤。  
  
4. 在 [記錄快照集]  頁面上，選取 [排程及設定]  按鈕。  
  
5. 在 [排程]  區段中，如果至少有一項選擇尚未選取，則請選取下列其中一或兩個選項：
    - **依排程建立歷程記錄快照集**。  
    - **允許人員手動建立快照集**。  
  
6. 在 [進階]  區段中，選取 [保留所有記錄快照集]  。  
  
7. 選擇性地選取 [也將快取快照集儲存至報表記錄]  的核取方塊。  
  
8.  選取 [套用]  以儲存設定。  

    > [!NOTE]  
    > 若要啟用建立快照集功能，系統管理員必須將報表記錄設定為 [允許手動建立記錄]  。 如需詳細資訊，請參閱[限制報表記錄 (入口網站)](../../reporting-services/reports/limit-report-history-report-manager.md)。

9.  按一下 [套用]  。

## <a name="to-automatically-add-all-snapshots-to-report-history"></a>若要自動將所有快照集加入報表記錄  
  
1. 若為已經設定成當做報表執行快照集執行的報表，您可以設定其他屬性，以便在每次重新整理快照集時，將快照集的副本儲存至報表記錄。  
  
2. 在入口網站中，巡覽至您想要檢視其記錄的項目，並以滑鼠右鍵按一下該項目。  
  
3. 從下拉式功能表中選取 [管理]  。  
  
4. 選取 [記錄快照集]  索引標籤。  
  
5. 在 [記錄快照集]  頁面上，選取 [排程及設定]  按鈕。  
  
6. 在 [排程]  區段中，如果至少有一項選擇尚未選取，則請選取下列其中一或兩個選項：
    - **依排程建立歷程記錄快照集**。  
    - **允許人員手動建立快照集**。  
  
7. 在 [進階]  區段中，選取 [保留所有記錄快照集]  。  
  
8. 選擇性地選取 [也將快取快照集儲存至報表記錄]  的核取方塊。  
  
9. 選取 [套用]  以儲存設定。  
  
## <a name="to-automatically-add-snapshots-to-report-history-based-on-a-schedule"></a>若要依照排程自動將快照集加入報表記錄  
  
1. 在入口網站中，巡覽至您想要檢視其記錄的項目，並以滑鼠右鍵按一下該項目。  
  
2. 從下拉式功能表中選取 [管理]  。  
  
3. 選取 [記錄快照集]  索引標籤。  
  
4. 在 [記錄快照集]  頁面上，選取 [排程及設定]  按鈕。  
  
5. 選取 **[使用下列排程將快照集加入至報表記錄]** 的核取方塊。 執行下列其中一項：  
  
    - 選取 [報表特定排程]  。 填入排程詳細資料，選取排程的開始和結束日期，然後按一下 **[確定]** 。  

    - 選取 **[共用排程]** 。 從清單中，選取喜好的排程。  

5. 按一下 [套用]  。  
  
## <a name="see-also"></a>另請參閱

- [設定報表的執行屬性 (入口網站)](../../reporting-services/reports/configure-execution-properties-for-a-report-report-manager.md)
- [限制報表記錄 (入口網站)](../../reporting-services/reports/limit-report-history-report-manager.md)
- [排程](../../reporting-services/subscriptions/schedules.md)   
- [入口網站 &#40;SSRS 原生模式&#41;](https://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)

::: moniker-end