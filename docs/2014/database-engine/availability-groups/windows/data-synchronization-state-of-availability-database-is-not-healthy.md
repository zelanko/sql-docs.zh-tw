---
title: 可用性資料庫的資料同步處理狀態不健全 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.agdashboard.arp3datasynchealthy.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 4fd003e7-808e-4b0e-b28a-47d9f2616f06
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 895e65f9538b588299520e9e22192935535b7931
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62815115"
---
# <a name="data-synchronization-state-of-availability-database-is-not-healthy"></a>可用性資料庫的資料同步處理狀態不健全
    
## <a name="introduction"></a>簡介  
  
|||  
|-|-|  
|**原則名稱**|可用性資料庫資料同步處理狀態|  
|**問題**|可用性資料庫的資料同步處理狀態不良。|  
|**類別**|**Warning**|  
|**層面**|可用性資料庫|  
  
## <a name="description"></a>描述  
 這項原則會積存可用性複本中所有可用性資料庫 (也稱為「資料庫複本」) 的資料同步處理狀態。 當任何資料庫複本不在預期的資料同步處理狀態時，原則為狀況不良。 否則原則為狀況良好。  
  
> [!NOTE]  
>  在此版本 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]中，可能原因和解決方案的資訊位於 TechNet Wiki 上的 [可用性資料庫的資料同步處理狀態不良](https://go.microsoft.com/fwlink/p/?LinkId=220858) 。  
  
## <a name="possible-causes"></a>可能的原因  
 此可用性資料庫的資料同步處理狀態不良。 在非同步認可可用性複本上，每個可用性資料庫都應該處於 SYNCHRONIZING 狀態。 在同步認可複本上，每個可用性資料庫都必須處於 SYNCHRONIZED 狀態。  
  
## <a name="possible-solution"></a>可能的解決方案  
 使用此資料庫複本原則，尋找資料同步處理狀態不良的資料庫複本，然後解決資料庫複本上的問題。  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組 &#40;SQL Server 的總覽&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [使用 AlwaysOn 儀表板 &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
