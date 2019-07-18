---
title: 暫停及繼續共用排程 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: subscriptions
ms.topic: conceptual
helpviewer_keywords:
- pausing schedules
- report-specific schedules [Reporting Services]
- shared schedules [Reporting Services], resuming
- resuming schedules
- continuing schedules
- schedules [Reporting Services], resuming
- schedules [Reporting Services], pausing
ms.assetid: e416be75-5234-4aa6-a3de-77f60f25169a
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7ec4c97ad3627ae91fd01cf0d8d73a2569a0c41a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65578173"
---
# <a name="pause-and-resume-shared-schedules"></a>Pause and Resume Shared Schedules
  您可以暫停並繼續使用中的共用排程。 暫停共用排程提供暫時凍結用於觸發報表處理與訂閱排程的方法。 只有共用排程可以暫停並繼續。 您無法暫停報表特定排程。  
  
 您不能暫停和繼續已在進行中的報表處理。 您只能暫停和繼續 SQL Server Agent 服務之排程佇列中的排程。 進行中的作業是在排程引擎的範圍之外。 如需詳細資訊，請參閱 [管理執行中的處理序](../../reporting-services/subscriptions/manage-a-running-process.md)  
  
 當共用排程暫停時，允許任何可能發生的作業失效。 繼續共用排程之後，報表和訂閱處理就會按照伺服器的當地時間，在下次排程的時間進行。 原生模式報表伺服器或 SharePoint 服務應用程式不會回頭處理在排程暫停期間原本應該執行的預定作業。  
  
 本主題內容：  
  
-   [暫停及繼續共用排程 (原生模式)](#bkmk_native)  
  
-   [暫停及繼續共用排程 (SharePoint 模式)](#bkmk_sharepoint)  
  
##  <a name="bkmk_native"></a> 暫停及繼續共用排程 (原生模式)  
 若要暫停和繼續共用排程，請使用報表管理員的 [排程] 頁面。 您不能使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]，因為它並未提供暫停和繼續排程的選項。 如需詳細資訊，請參閱 [Create, Modify, and Delete Schedules](../../reporting-services/subscriptions/create-modify-and-delete-schedules.md)。  
  
#### <a name="to-pause-or-resume-a-shared-schedule"></a>若要暫停或繼續共用排程  
  
1.  從報表管理員中，按一下 **[站台設定]** 。  
  
2.  按一下 **[排程]** 。  
  
3.  選取排程，然後按一下功能區中的 **[暫停]** 或 **[繼續]** 。 如果排程目前為暫停狀態，則 **[狀態]** 資料行將包含 **[已暫停]** 。  
  
##  <a name="bkmk_sharepoint"></a> 暫停及繼續共用排程 (SharePoint 模式)  
 若要暫停及繼續共用排程，請使用 [站台設定] 頁面或 PowerShell。 排程是以每個 SharePoint 網站為單位管理。  
  
#### <a name="to-pause-or-resume-a-shared-schedule"></a>若要暫停或繼續共用排程  
  
1.  按一下 **[網站動作]** 。  
  
2.  按一下 **[站台設定]** 。  
  
3.  在 [Reporting Services] 區段中，按一下 **[管理共用排程]** 。  
  
4.  選取排程，然後按一下 **[暫停選取的排程]** 或 **[執行選取的排程]** 。 如果排程目前為暫停狀態，則 **[狀態]** 資料行將包含 **[已暫停]** 。  
  
## <a name="see-also"></a>另請參閱  
 [[排程]](../../reporting-services/subscriptions/schedules.md)   
 [Create, Modify, and Delete Schedules](../../reporting-services/subscriptions/create-modify-and-delete-schedules.md)   
 [變更報表伺服器上的時區和時鐘設定](../../reporting-services/subscriptions/change-time-zones-and-clock-settings-on-a-report-server.md)   
 [管理執行中的處理序](../../reporting-services/subscriptions/manage-a-running-process.md)  
  
  
