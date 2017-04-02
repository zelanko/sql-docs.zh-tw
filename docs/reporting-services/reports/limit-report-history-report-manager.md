---
title: "限制報表記錄 (報表管理員) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "檢視報表記錄"
  - "報表記錄 [Reporting Services], 檢視記錄"
  - "報表記錄 [Reporting Services], 設定記錄"
  - "記錄資料 [Reporting Services]"
  - "顯示報表記錄"
ms.assetid: 8e255792-d9ef-496f-a26c-9e969c1209a0
caps.latest.revision: 36
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 36
---
# 限制報表記錄 (報表管理員)
  報表記錄是您在經過一段時間後建立之報表快照集的集合。 您可以視需要建立報表記錄，或是排程在報表記錄中建立和加入快照集的頻率。  
  
 報表記錄會儲存在報表伺服器資料庫中。 如果報表快照集包含大量資料，您可能會考慮限制報表記錄，以便盡可能減少快照集保留對資料庫大小的影響。  
  
### 若要設定報表伺服器的報表記錄  
  
1.  在報表管理員中，按一下全域工具列上的 [站台設定]。  
  
2.  若要無限地保存所有報表記錄，請選取 [不限制報表記錄中的快照集數目]。 否則，請選取 [限制報表記錄的副本]，指定可以為任一給定報表保存的快照集最大數目。  
  
3.  按一下 **[套用]**。  
  
### 若要設定特定報表的報表記錄  
  
1.  在報表管理員中，導覽至您要設定記錄的報表，然後按一下該報表來開啟它。  
  
2.  按一下 **[屬性]** 索引標籤。  
  
3.  按一下 [記錄] 索引標籤。  
  
4.  選取報表的選項，然後按一下 [套用]。 如需每個選項的詳細資訊，請參閱[快照集選項屬性頁 &#40;報表管理員&#41;](../Topic/Snapshot%20Options%20Properties%20Page%20\(Report%20Manager\).md)。  
  
## 請參閱＜  
 [將快照集加入報表記錄 &#40;報表管理員&#41;](../../reporting-services/report-server/add-a-snapshot-to-report-history-report-manager.md)   
 [報表管理員 &#40;SSRS 原生模式&#41;](../Topic/Report%20Manager%20%20\(SSRS%20Native%20Mode\).md)  
  
  