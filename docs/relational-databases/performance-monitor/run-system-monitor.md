---
title: 執行活動監視器 | Microsoft 文件
description: 系統監視器使用遠端程序呼叫從 SQL Server 收集資訊。 任何具有執行系統監視器權限的使用者都可監視 SQL Server。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- System Monitor [SQL Server], running
- Windows System Monitor [SQL Server], running
- remote procedure calls [SQL Server]
- starting Windows NT System Monitor
- RPC
ms.assetid: 05297984-bc8d-43df-829c-032387f7ea61
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: ee6fb05d0ec83fe38acbef4ad80494c3a4a5c975
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505962"
---
# <a name="run-system-monitor"></a>執行系統監視器
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  「系統監視器」會使用遠端程序呼叫 (RPC) 從 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]收集資訊。 任何擁有 Microsoft Windows 權限可執行「系統監視器」的使用者都可以使用「系統監視器」來監視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
> [!NOTE]  
>  在使用「系統監視器」或「效能監視器」時，您不能連接到在 Windows 98 上執行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。  
  
 「系統監視器」和所有的效能監視工具一樣，當使用系統監視器監視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時，必定會對某些效能帶來額外負擔。 任何特定執行個體的實際負擔取決於硬體平台、計數器數目與選取的更新間隔。 但是，整合「系統監視器」與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的目的是要將會致使效能變差的影響降到最低。  
  
> [!NOTE]  
>  若已在「系統監視器」嵌入式管理單元中選取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 效能計數器來進行監視，即使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不在執行中，您也會看到計數器。  
  
 如需啟動「系統監視器」的詳細資訊，請參閱[啟動系統監視器 &#40;Windows&#41;](../../relational-databases/performance/start-system-monitor-windows.md)。  
  
  
