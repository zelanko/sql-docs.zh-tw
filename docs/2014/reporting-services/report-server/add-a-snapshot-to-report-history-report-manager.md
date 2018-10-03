---
title: 將快照集新增至報表記錄 (報表管理員) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- report history [Reporting Services], adding snapshots
- historical data [Reporting Services]
- snapshots [Reporting Services], adding report snapshots
- adding snapshots to report history
- report snapshots [Reporting Services], adding
ms.assetid: 3aafb183-789e-46ac-966c-881dc549b31d
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: e0c9e553ebff35c865adabfeea164a56b5cffce0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48075968"
---
# <a name="add-a-snapshot-to-report-history-report-manager"></a>將快照集加入報表記錄 (報表管理員)
  報表記錄是您在經過一段時間後建立之報表快照集的集合。 報表快照集是一種報表，它包含在特定時間點擷取的配置資訊和查詢結果。 報表快照集和視需要報表不同，視需要報表會在您選取報表時取得最新的查詢結果，而報表快照集是依排程處理，並儲存至報表伺服器。 您選取報表快照集以供檢視時，報表伺服器會從報表伺服器資料庫擷取儲存的報表，並顯示建立快照集當時的資料與配置。  
  
 報表快照集不會以特定轉譯格式儲存。 而是只有在使用者或應用程式要求它時，報表快照集才以最後的檢視格式轉譯 (例如 HTML)。 延遲轉譯讓快照集具有可攜性。 報表可以使用要求的裝置或 Web 瀏覽器的正確格式轉譯。  
  
### <a name="to-manually-add-snapshots-to-report-history"></a>若要手動將快照集加入至報表記錄  
  
1.  在報表管理員中，巡覽至 [內容] 頁面，將滑鼠游標停留在您想要檢視記錄的項目上方，然後按一下下拉箭號。  
  
2.  在下拉式功能表中，按一下 **[檢視報表記錄]**。  
  
3.  按一下 **[新增快照集]**。 **[執行時]** 資料行裡會建立一個新的快照集。  
  
    > [!NOTE]  
    >  管理員必須將報表記錄設定為 **[允許手動建立記錄]**，才能執行此作業。 如需詳細資訊，請參閱 <<c0> [ 限制報表記錄&#40;報表管理員&#41;](../reports/limit-report-history-report-manager.md)。</c0>  
  
4.  按一下 **[套用]**。  
  
### <a name="to-automatically-add-all-snapshots-to-report-history"></a>若要自動將所有快照集加入報表記錄  
  
1.  若為已經設定成當做報表執行快照集執行的報表，您可以設定其他屬性，以便在每次重新整理快照集時，將快照集的副本儲存至報表記錄。  
  
2.  在報表管理員中，巡覽至 [內容] 頁面，將滑鼠游標停留在您想要檢視記錄的項目上方，然後按一下下拉箭號。  
  
3.  在下拉式功能表中，按一下 **[管理]**。  
  
4.  按一下 **[快照集選項]**。  
  
5.  選取 **[將所有報表執行快照集儲存在記錄中]** 的核取方塊。  
  
6.  按一下 **[套用]**。  
  
### <a name="to-automatically-add-snapshots-to-report-history-based-on-a-schedule"></a>若要依照排程自動將快照集加入報表記錄  
  
1.  在報表管理員中，巡覽至 [內容] 頁面，將滑鼠游標停留在您想要檢視記錄的項目上方，然後按一下下拉箭號。  
  
2.  在下拉式功能表中，按一下 **[管理]**。  
  
3.  按一下 **[快照集選項]**。  
  
4.  選取 **[使用下列排程將快照集加入至報表記錄]** 的核取方塊。 執行下列其中之一：  
  
    -   選取 [報表特定排程]。 填入排程詳細資料，選取排程的開始和結束日期，然後按一下 **[確定]**。  
  
    -   選取 **[共用排程]**。 從清單中，選取喜好的排程。  
  
5.  按一下 **[套用]**。  
  
## <a name="see-also"></a>另請參閱  
 [設定報表執行屬性&#40;報表管理員&#41;](../reports/configure-execution-properties-for-a-report-report-manager.md)   
 [開啟及關閉報表&#40;報表管理員&#41;](../reports/open-and-close-a-report-report-manager.md)   
 [限制報表記錄 &#40;報表管理員&#41;](../reports/limit-report-history-report-manager.md)   
 [[排程]](../subscriptions/schedules.md)   
 [報表管理員 &#40;SSRS 原生模式&#41;](../report-manager-ssrs-native-mode.md)  
  
  
