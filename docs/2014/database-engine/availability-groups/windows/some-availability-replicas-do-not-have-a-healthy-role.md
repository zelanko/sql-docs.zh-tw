---
title: 某些可用性複本沒有狀況良好的角色 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.agdashboard.agp6allroleshealthy.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 7ec5b337-7201-4a66-a541-7560f8b18784
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 50518e78585b7e56f62411edc539d0f9ac3db9e9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62788182"
---
# <a name="some-availability-replicas-do-not-have-a-healthy-role"></a>某些可用性複本沒有狀況良好的角色
    
## <a name="introduction"></a>簡介  
  
|||  
|-|-|  
|**原則名稱**|可用性複本角色狀態|  
|**問題**|某些可用性複本沒有狀況良好的角色。|  
|**類別目錄**|**警告**|  
|**Facet**|可用性群組|  
  
## <a name="description"></a>描述  
 這項原則會積存所有可用性複本的連接狀態，並檢查是否有任何可用性複本沒有狀況良好的角色。 當可用性複本既不是主要也不是次要時，原則為狀況不良。 否則原則為狀況良好。  
  
> [!NOTE]  
>  在此版本 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]中，可能原因和解決方案的資訊位於 TechNet Wiki 上的 [某些可用性複本沒有狀況良好的角色](https://go.microsoft.com/fwlink/p/?LinkId=220854) 。  
  
## <a name="possible-causes"></a>可能的原因  
 在此可用性群組中，至少一個可用性複本目前沒有主要或次要角色。  
  
## <a name="possible-solution"></a>可能的解決方案  
 使用可用性複本原則狀態，尋找其角色不是主要或次要的可用性複本，然後解決可用性複本上的問題。  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組 &#40;SQL Server 的總覽&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [使用 AlwaysOn 儀表板 &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
