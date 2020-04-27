---
title: 作業活動監視器 (篩選設定) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql12.swb.jobactivitymon.filter.f1
ms.assetid: 89cb0055-5262-447f-8464-7203d4caba78
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b6c7b5cff8b288e688f2744c615d62bd8417acf5
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62856646"
---
# <a name="job-activity-monitor-filter-settings"></a>作業活動監視器 (篩選設定)
  使用此頁面來減少可以在作業活動監視器看到的資料列數目。 在一或數個可用的方塊中輸入準則，只顯示符合指定值的資料列。 有些方塊 (例如 [狀態]  或 [封鎖類型]  ) 提供有限數目的可能值，經由下拉式清單提供。 其他的方塊 (例如 [應用程式]  ) 則允許您以逗號分隔的清單，輸入任何值以及隨您想要之數量的值。 工具列圖示允許您依類別或字母順序排序可用的方塊。 按一下準則以顯示每個準則的簡短描述。  
  
 若要篩選作業活動監視器，請依照需要提供篩選準則，並按一下 [套用篩選]  ，然後按一下 [確定]  。  
  
## <a name="all-jobs"></a>所有作業  
 這組篩選準則可在篩選作業活動監視器時使用。  
  
 **名稱**  
 依名稱篩選作業。  
  
 **下次執行**  
 依下一個排程的執行日期篩選。  
  
 **可執行的**  
 檢視可以執行的作業，或無法執行的作業。 選取 [是]  只能檢視可以執行的作業，選取 [否]  只能檢視無法執行的作業，選取 [全部]  則能同時檢視可以執行與無法執行的作業。  
  
 **最後執行**  
 依上次執行日期篩選。  
  
 **上次執行結果**  
 依上次執行作業的狀態篩選作業。  
  
 **已啟用**  
 只檢視已啟用或未啟用的作業  
  
 **類別目錄**  
 依作業類別目錄篩選作業。  
  
 **已排程**  
 檢視具有排程或無排程的所有作業。  
  
 **狀態**  
 依狀態篩選作業。  
  
## <a name="description-area"></a>描述區域  
 **描述方塊**  
 這個未命名的方塊，在準則被選取時提供準則的簡短描述。  
  
 **套用篩選**  
 若要套用篩選，請按一下 [套用**篩選**]，然後按一下 **[確定]**。 若要在 [**篩選設定**] 對話方塊中保留篩選設定，但不套用它們，請取消選取 [套用**篩選**]，然後按一下 **[確定]** 以顯示所有資料列。  
  
 **Clear**  
 將篩選設定恢復成預設值。  
  
## <a name="see-also"></a>另請參閱  
 [監視作業活動](../../ssms/agent/monitor-job-activity.md)  
  
  
