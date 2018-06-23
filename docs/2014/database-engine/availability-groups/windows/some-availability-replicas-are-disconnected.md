---
title: 部分可用性複本已中斷連接 | Microsoft Docs
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
- sql12.swb.agdashboard.agp7allconnected.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: aea808be-6f0f-40c2-9aa2-a2a435ec6443
caps.latest.revision: 10
author: rothja
ms.author: jroth
manager: jhubbard
ms.openlocfilehash: 1705fdc26d1a0fe51b7a18ee4fa6e740c56cc24b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36037536"
---
# <a name="some-availability-replicas-are-disconnected"></a>部分可用性複本已中斷連接
    
## <a name="introduction"></a>簡介  
  
|||  
|-|-|  
|**原則名稱**|可用性複本連接狀態|  
|**問題**|某些可用性複本已中斷連接。|  
|**類別目錄**|**警告**|  
|**Facet**|可用性群組|  
  
## <a name="description"></a>描述  
 這項原則會積存所有可用性複本的連接狀態，並檢查是否有任何 DISCONENCTED 的可用性複本。 當任何可用性複本為 DISCONNECTED 時，原則為狀況不良。 否則原則為狀況良好。  
  
> [!NOTE]  
>  在此版本的 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]中，可能原因和解決方案的資訊位於 TechNet Wiki 上的 [某些可用性複本已中斷連接](http://go.microsoft.com/fwlink/p/?LinkId=220855) 。  
  
## <a name="possible-causes"></a>可能的原因  
 在此可用性群組中，至少一個次要複本未連接至主要複本。 連接狀態為 DISCONNECTED。  
  
## <a name="possible-solution"></a>可能的解決方案  
 使用可用性複本原則狀態，尋找 DISCONNECTED 的可用性複本，然後解決可用性複本上的問題。  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組概觀&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [使用 AlwaysOn 儀表板 &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  