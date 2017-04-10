---
title: "可用性複本已中斷連接 | Microsoft Docs"
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
  - "sql13.swb.agdashboard.arp2connected.issues.f1"
helpviewer_keywords: 
  - "可用性群組 [SQL Server], 原則"
ms.assetid: 1a2162d3-54fb-4356-b349-effbdc15a5a4
caps.latest.revision: 12
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 12
---
# 可用性複本已中斷連接
    
## 簡介  
  
|||  
|-|-|  
|**原則名稱**|可用性複本連接狀態|  
|**問題**|可用性複本已中斷連接。|  
|**類別目錄**|**嚴重**|  
|**Facet**|可用性複本|  
  
## 描述  
 這項原則檢查可用性複本之間的連接狀態。 當可用性複本的連接狀態為 DISCONNECTED 時，原則為狀況不良。 否則原則為狀況良好。  
  
> [!NOTE]  
>  在此 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 版本中，可能原因和解決方案的資訊位於 TechNet Wiki 上的 [Availability replica is disconnected](http://go.microsoft.com/fwlink/p/?LinkId=220857) (可用性複本已中斷連接)。  
  
## 可能的原因  
 次要複本未連接到主要複本。 連接狀態為 DISCONNECTED。 這個問題可能是由於下列原因所造成：  
  
-   連接通訊埠可能與另一個應用程式衝突。  
  
-   加密類型或演算法不符。  
  
-   連接端點已刪除或尚未啟動。  
  
-   傳輸已中斷連接。  
  
## 可能的解決方案  
 此問題的可能解決方案如下：  
  
-   檢查主要複本與次要複本執行個體的資料庫鏡像端點組態，並更新不符的組態。  
  
-   檢查通訊埠是否相衝突，如果是，則變更通訊埠編號。  
  
## 另請參閱  
 [AlwaysOn 可用性群組概觀 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [使用 AlwaysOn 儀表板 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  