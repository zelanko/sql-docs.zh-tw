---
title: 作業活動監視器重新整理 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.jobactivitymon.refresh.f1
ms.assetid: 413a368e-fd2b-4e1f-b370-002cdbc85bab
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 9e31951f2e0bd3c954ae7ee1fb20d1a982005603
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36037013"
---
# <a name="job-activity-monitor-refresh"></a>作業活動監視器重新整理
  使用 **[重新整理設定]** 對話方塊，設定作業活動監視器取得有關伺服器活動新資訊的頻率。 作業活動監視器必須在監視的伺服器上執行查詢，以取得作業活動監視器方格的資訊。 自動重新整理間隔的設定小於 30 秒時，用來執行這些查詢的時間就會影響伺服器效能。  
  
 若要開啟此對話方塊，請在作業活動監視器的 **[狀態]** 區段中按一下 **[檢視重新整理設定]** 。  
  
## <a name="options"></a>選項。  
 **自動重新整理間隔**  
 勾選即可起始活動監視器資訊的自動重新整理功能。 依預設，此功能是關閉的。  
  
 **seconds**  
 嘗試進行自動重新整理的間隔秒數。 預設值是 60 秒。 值設定為 5 或小於 5 時，表示每隔 5 秒進行重新整理。  
  
## <a name="see-also"></a>另請參閱  
 [監視作業活動](../../ssms/agent/monitor-job-activity.md)  
  
  