---
title: "可用性資料庫已暫停 | Microsoft Docs"
ms.custom: ""
ms.date: "05/17/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.agdashboard.drp1notsuspended.issues.f1"
helpviewer_keywords: 
  - "可用性群組 [SQL Server], 原則"
ms.assetid: 6baee70f-848c-4e86-b20d-78875c0f82cb
caps.latest.revision: 15
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 15
---
# 可用性資料庫已暫停
    
## 簡介  
  
|||  
|-|-|  
|**原則名稱**|可用性資料庫暫停狀態|  
|**問題**|可用性資料庫已暫停。|  
|**類別目錄**|**警告**|  
|**Facet**|可用性資料庫|  
  
## 描述  
 此原則會檢查次要資料庫 (也稱為「次要資料庫複本」) 的資料移動。 當資料移動已暫停時，原則為狀況不良。 否則原則為狀況良好。  
  
> [!NOTE]  
>  在此版本 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 中，可能原因和解決方案的資訊位於 TechNet Wiki 上的[可用性資料庫已暫停](http://go.microsoft.com/fwlink/p/?LinkId=220860)。  
  
## 可能的原因  
 由於下列原因，此可用性資料庫上的資料同步處理可能已暫停：  
  
-   由於錯誤，系統可能已暫停資料同步處理。  
  
-   資料庫管理員可能為了進行維護已暫停資料同步處理。  
  
## 可能的解決方案  
 繼續資料同步處理。 如果問題仍然存在，請檢查事件記錄檔中的可用性群組，然後診斷為什麼系統暫停資料移動。  
  
## 另請參閱  
 [AlwaysOn 可用性群組概觀 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [使用 AlwaysOn 儀表板 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  