---
title: 部分可用性複本未同步處理資料 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.agdashboard.agp4synchronizing.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 3db6a569-e942-4321-a0dd-c4ab002087c8
caps.latest.revision: 10
author: rothja
ms.author: jroth
manager: jhubbard
ms.openlocfilehash: fca9b4327084689bd6df29b86462fd0227564f80
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36134248"
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
 [AlwaysOn 可用性群組概觀&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [使用 AlwaysOn 儀表板 &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  