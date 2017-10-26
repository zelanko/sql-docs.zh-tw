---
title: "部分可用性複本未同步處理資料 | Microsoft Docs"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.agdashboard.agp4synchronizing.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 3db6a569-e942-4321-a0dd-c4ab002087c8
caps.latest.revision: 12
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 28ef1fac4a5497b94dcc22c0509fb1e923667014
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="some-availability-replicas-are-not-synchronizing-data"></a>部分可用性複本未同步處理資料
    
## <a name="introduction"></a>簡介  
  
|||  
|-|-|  
|**原則名稱**|可用性複本資料同步處理狀態|  
|**問題**|某些可用性複本並未同步處理資料。|  
|**類別目錄**|**警告**|  
|**Facet**|可用性群組|  
  
## <a name="description"></a>描述  
 這項原則會積存可用性群組中所有可用性複本的資料同步處理狀態，並檢查是否有任何可用性複本的同步處理無法運作。 如果可用性複本的任何資料同步處理狀態為 NOT SYNCHRONIZING，原則為狀況不良。  
  
 如果可用性複本的任何資料同步處理狀態都不是 NOT SYNCHRONIZING，此原則為狀況良好。  
  
> [!NOTE]  
>  在此版本 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]中，可能原因和解決方案的資訊位於 TechNet Wiki 上的 [某些可用性複本並未同步處理資料](http://go.microsoft.com/fwlink/p/?LinkId=220852) 。  
  
## <a name="possible-causes"></a>可能的原因  
 在這個可用性群組中，至少有一個次要複本具有 NOT SYNCHRONIZING 同步處理狀態，而且並未收到來自主要複本的資料。  
  
## <a name="possible-solution"></a>可能的解決方案  
 使用可用性複本原則狀態，尋找具有 NOT SYNCHROINIZING 狀態的可用性複本，然後解決可用性複本上的問題。  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組概觀 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [使用 Always On 儀表板 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  

