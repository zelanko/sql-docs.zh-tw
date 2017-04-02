---
title: "次要資料庫未加入 | Microsoft Docs"
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
  - "sql13.swb.agdashboard.drp2joined.issues.f1"
helpviewer_keywords: 
  - "可用性群組 [SQL Server], 原則"
ms.assetid: 10817e5e-75fa-42dd-baa2-359bea3ad051
caps.latest.revision: 14
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 14
---
# 次要資料庫未加入
    
## 簡介  
  
|||  
|-|-|  
|**原則名稱**|可用性資料庫聯結狀態|  
|**問題**|次要資料庫並未聯結。|  
|**類別目錄**|**警告**|  
|**Facet**|可用性資料庫|  
  
## 描述  
 此原則會檢查次要資料庫 (也稱為「次要資料庫複本」) 的聯結狀態。 當資料庫複本未聯結時，原則為狀況不良。 否則原則為狀況良好。  
  
> [!NOTE]  
>  在此 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 版本中，可能原因和解決方案的資訊位於 TechNet Wiki 上的 [Secondary database is not joined](http://go.microsoft.com/fwlink/p/?LinkId=220862) (次要資料庫並未聯結)。  
  
## 可能的原因  
 此次要資料庫並未聯結至可用性群組。 此次要資料庫的組態不完整。  
  
## 可能的解決方案  
 使用 Transact-SQL、PowerShell 或 SQL Server Management Studio，將次要複本聯結至可用性群組。 如需將次要複本聯結至可用性群組的詳細資訊，請參閱[將次要複本聯結至可用性群組 (SQL Server)](http://msdn.microsoft.com/library/ff878473\(SQL.110\).aspx)。  
  
## 另請參閱  
 [AlwaysOn 可用性群組概觀 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [使用 AlwaysOn 儀表板 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  