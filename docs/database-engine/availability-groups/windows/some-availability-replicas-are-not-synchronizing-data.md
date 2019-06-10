---
title: 部分可用性複本未同步處理資料 | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.agdashboard.agp4synchronizing.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 3db6a569-e942-4321-a0dd-c4ab002087c8
author: MashaMSFT
ms.author: mathoma
manager: jroth
ms.openlocfilehash: d16917d5b22189be5ffcbe48260fd7cc9b68c42e
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66794301"
---
# <a name="some-availability-replicas-are-not-synchronizing-data"></a>部分可用性複本未同步處理資料
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="introduction"></a>簡介  
  
|||  
|-|-|  
|**原則名稱**|可用性複本資料同步處理狀態|  
|**問題**|某些可用性複本並未同步處理資料。|  
|**類別目錄**|**警告**|  
|**Facet**|可用性群組|  
  
## <a name="description"></a>Description  
 這項原則會積存可用性群組中所有可用性複本的資料同步處理狀態，並檢查是否有任何可用性複本的同步處理無法運作。 如果可用性複本的任何資料同步處理狀態為 NOT SYNCHRONIZING，原則為狀況不良。  
  
 如果可用性複本的任何資料同步處理狀態都不是 NOT SYNCHRONIZING，此原則為狀況良好。  
  
> [!NOTE]  
>  在此版本 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]中，可能原因和解決方案的資訊位於 TechNet Wiki 上的 [某些可用性複本並未同步處理資料](https://go.microsoft.com/fwlink/p/?LinkId=220852) 。  
  
## <a name="possible-causes"></a>可能的原因  
 在這個可用性群組中，至少有一個次要複本具有 NOT SYNCHRONIZING 同步處理狀態，而且並未收到來自主要複本的資料。  
  
## <a name="possible-solution"></a>可能的解決方案  
 使用可用性複本原則狀態，尋找具有 NOT SYNCHROINIZING 狀態的可用性複本，然後解決可用性複本上的問題。  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組概觀 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [使用 AlwaysOn 儀表板 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
