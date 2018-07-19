---
title: 可用性複本已中斷連接 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.agdashboard.arp2connected.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 1a2162d3-54fb-4356-b349-effbdc15a5a4
caps.latest.revision: 10
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 45c1441441181b5a904f4f2d9370e9c3b9328789
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37265318"
---
# <a name="availability-replica-is-disconnected"></a>可用性複本已中斷連接
    
## <a name="introduction"></a>簡介  
  
|||  
|-|-|  
|**原則名稱**|可用性複本連接狀態|  
|**問題**|可用性複本已中斷連接。|  
|**類別目錄**|**嚴重**|  
|**Facet**|可用性複本|  
  
## <a name="description"></a>描述  
 這項原則檢查可用性複本之間的連接狀態。 當可用性複本的連接狀態為 DISCONNECTED 時，原則為狀況不良。 否則原則為狀況良好。  
  
> [!NOTE]  
>  在此 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]版本中，可能原因和解決方案的資訊位於 TechNet Wiki 上的 [Availability replica is disconnected](http://go.microsoft.com/fwlink/p/?LinkId=220857) (可用性複本已中斷連接)。  
  
## <a name="possible-causes"></a>可能的原因  
 次要複本未連接到主要複本。 連接狀態為 DISCONNECTED。 這個問題可能是由於下列原因所造成：  
  
-   連接通訊埠可能與另一個應用程式衝突。  
  
-   加密類型或演算法不符。  
  
-   連接端點已刪除或尚未啟動。  
  
-   傳輸已中斷連接。  
  
## <a name="possible-solutions"></a>可能的解決方案  
 此問題的可能解決方案如下：  
  
-   檢查主要複本與次要複本執行個體的資料庫鏡像端點組態，並更新不符的組態。  
  
-   檢查通訊埠是否相衝突，如果是，則變更通訊埠編號。  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組概觀&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [使用 AlwaysOn 儀表板 &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
