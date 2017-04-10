---
title: "可用性複本未聯結 | Microsoft Docs"
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
  - "sql13.swb.agdashboard.arp4joined.issues.f1"
helpviewer_keywords: 
  - "可用性群組 [SQL Server], 原則"
ms.assetid: 9c0d10b1-9e12-430c-83b9-ca2bd0a3afc4
caps.latest.revision: 15
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 15
---
# 可用性複本未聯結
    
## 簡介  
  
|||  
|-|-|  
|**原則名稱**|可用性複本聯結狀態|  
|**問題**|可用性複本未聯結。|  
|**類別目錄**|**警告**|  
|**Facet**|可用性複本|  
  
## 描述  
 這項原則會檢查可用性複本的聯結狀態。 當可用性複本已加入至可用性角色，但是沒有正確聯結時，原則為狀況不良。 否則原則為狀況良好。  
  
> [!NOTE]  
>  在此 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 版本中，可能原因和解決方案的資訊位於 TechNet Wiki 上的 [Availability replica is not joined](http://go.microsoft.com/fwlink/p/?LinkId=220859) (可用性複本未聯結)。  
  
## 可能的原因  
 次要複本並未聯結至可用性群組。 若要讓可用性複本成功聯結至可用性群組，聯結狀態必須是聯結的獨立執行個體 (1) 或聯結的容錯移轉叢集 (2)。  
  
## 可能的解決方案  
 使用 Transact-SQL、PowerShell 或 SQL Server Management Studio，將次要複本聯結至可用性群組。 如需將次要複本聯結至可用性群組的詳細資訊，請參閱[將次要複本聯結至可用性群組 (SQL Server)](http://msdn.microsoft.com/library/ff878473\(SQL.110\).aspx)。  
  
## 另請參閱  
 [AlwaysOn 可用性群組概觀 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [使用 AlwaysOn 儀表板 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  