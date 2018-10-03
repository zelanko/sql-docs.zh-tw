---
title: 作業活動監視器 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- SQL12.SWB.ACTIVITYMON.F1
- sql12.ag.jobactivitymonitor.alljobs.f1
ms.assetid: 11f2182c-5f71-46f8-8d2b-74f0fc48f2d6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 33a5730066cd18cf32a294fdc272e09b629d35af
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48206048"
---
# <a name="job-activity-monitor"></a>作業活動監視器
  使用此頁面即可檢視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業的目前活動。 按一下 [篩選] 即可限制顯示的作業。 [代理程式作業活動] 方格是唯讀的。 按一下資料行標頭即可排序方格。 若要修改作業，請按兩下作業以開啟 [作業屬性] 對話方塊。 以滑鼠右鍵按一下方格中的作業，即可開始執行所有作業步驟、於特定作業步驟開始、停用或啟用作業、重新整理作業、刪除作業、檢視作業的記錄或檢視作業的屬性。 按一下 [重新整理]，以最新資訊更新方格。  
  
## <a name="options"></a>選項。  
 **名稱**  
 作業名稱。  
  
 **已啟用**  
 不論作業為已啟用 ([是]) 或未啟用 ([否])。  
  
 **狀態** <sup>1</sup>  
 作業的目前狀態。  
  
 **上次執行結果**  
 作業上次執行的狀態。  
  
 **最後執行**  
 上次使用伺服器的當地日期和時間執行作業的日期和時間。  
  
 **接下來執行** <sup>1</sup>  
 下次排程為使用伺服器的當地日期和時間執行作業的日期和時間。  
  
 **類別目錄**  
 指派給作業的作業類別目錄。  
  
 **可執行的**  
 [是] 如果作業可執行；[否] 如果作業無法執行。 如果作業沒有任何步驟，或者沒有目標伺服器，就無法執行此作業。  
  
 **已排程**  
 [是] 表示作業已指派給作業排程；[否] 表示作業沒有排程。  
  
 <sup>1</sup>只有成員[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]sysadmin 固定伺服器角色和伺服器管理員可以看到群組值在這個資料行中。 SQLAgentOperatorRole 角色的成員無法看到此資料行中的值。  
  
#### <a name="to-open-the-job-activity-monitor"></a>若要開啟作業活動監視器  
  
-   在物件總管中，依序展開伺服器和 [SQL Server Agent]、以滑鼠右鍵按一下 [作業活動監視器]，然後按一下 [檢視作業活動]。  
  
## <a name="see-also"></a>另請參閱  
 [監視作業活動](monitor-job-activity.md)  
  
  
