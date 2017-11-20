---
title: "進度頁面 (AlwaysOn 可用性群組精靈) | Microsoft Docs"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: availability-groups
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.failoverwizard.progress.f1
- sql13.swb.adddatabasewizard.progress.f1
- sql13.swb.addreplicawizard.progress.f1
- sql13.swb.newagwizard.progress.f1
ms.assetid: bd3b0306-8384-4120-a1c9-03825f0ae26a
caps.latest.revision: 13
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 78fd0315e1f58eef1dbc5d8c41f6254817879d8c
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="progress-page-always-on-availability-group-wizards"></a>進度頁面 (AlwaysOn 可用性群組精靈)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  使用此對話方塊可以檢視您在 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 中執行之 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]精靈的進度。 進度列會指出精靈所執行之步驟的相對進度。  
  
## <a name="uielement-list"></a>UIElement 清單  
 **更多詳細資料**  
 按一下向下箭號可顯示進度方格，這個方格會依照順序列出任何已完成的步驟，接著列出目前進行中的作業。 方格包含下列資料行：  
  
 **名稱**  
 顯示描述特定步驟的片語。  
  
 **狀態**  
 指出已完成步驟的結果以及目前步驟的完成百分比，如下所示：  
  
|結果|描述|  
|------------|-----------------|  
|**錯誤**|表示這個步驟的作業發生錯誤。 按一下連結可顯示描述錯誤的訊息對話方塊。|  
|**進行中 (** *完成百分比* **)**|表示作業目前正在進行，並且估計這個步驟已完成的百分比。|  
|**成功**|表示這個步驟的作業已順利完成。|  
  
 **較少詳細資料**  
 按一下可隱藏進度方格。  
  
 **取消**  
 按一下可略過任何其餘作業，然後結束精靈。  
  
##  <a name="RelatedTasks"></a> 相關工作  
  
-   [使用新增可用性群組對話方塊 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [使用 [將複本加入可用性群組中精靈] &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
-   [使用 [將資料庫加入可用性群組中精靈] &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/availability-group-add-database-to-group-wizard.md)  
  
-   [使用容錯移轉可用性群組精靈 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-fail-over-availability-group-wizard-sql-server-management-studio.md)  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組概觀 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  

