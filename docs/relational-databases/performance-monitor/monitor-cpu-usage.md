---
title: 監視 CPU 使用量 |Microsoft Docs
description: 定期監視 SQL Server 執行個體，以判斷 CPU 使用率是否在正常範圍內。 使用系統監視器來查看 CPU 花費在執行執行緒上的時間。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- monitoring performance [SQL Server], CPU usage
- tuning databases [SQL Server], CPU usage
- processors [SQL Server], monitoring usage
- database performance [SQL Server], CPU usage
- monitoring CPU usage [SQL Server]
- server performance [SQL Server], CPU usage
- database monitoring [SQL Server], CPU usage
- monitoring [SQL Server], CPU usage
- processors [SQL Server]
- CPU [SQL Server], monitoring
- monitoring server performance [SQL Server], CPU usage
ms.assetid: 2a02a3b6-07b2-4ad0-8a24-670414d19812
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 2e81db69a70a54365ffe7da6fbe9933bb98848db
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/17/2020
ms.locfileid: "86458553"
---
# <a name="monitor-cpu-usage"></a>監視 CPU 使用量
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  請定期監視 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，以判定 CPU 使用率是否在正常範圍內。 持續偏高的 CPU 使用量比率可能代表必須將 CPU 升級，或增加多個處理器。 此外，偏高的 CPU 使用率可能代表應用程式的微調或設計不良。 將應用程式最佳化後可降低 CPU 的使用率。  
  
 使用「系統監視器」中的 **Processor:% Processor Time** 計數器是判定 CPU 使用量的一種有效方法。 此計數器可監視 CPU 花費在執行非閒置執行緒上的時間量。 狀態維持在 80% 到 90%，可能代表必須將 CPU 升級或增加更多處理器。 使用多處理器系統時，可針對每個處理器監視此計數器的不同執行個體。 此值代表特定處理器上的處理器時間總和。 若要判定所有處理器的平均值，請改為使用 **System: %Total Processor Time** 計數器。  
  
 (選擇性) 您也可以監視下列計數器，來監視處理器使用量：  
  
-   **Processor: % Privileged Time**  
  
     相當於處理器花費在執行 Microsoft Windows 核心命令 (如處理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] I/O 要求) 的時間百分比。 當 **Physical Disk** 計數器很高時，如果這個計數器也持續偏高，請考慮換用較快或較有效率的磁碟子系統 (Disk Subsystem)。  
  
    > [!NOTE]  
    >  不同的磁碟控制器和驅動程式會使用不同的核心處理 (kernel Process) 時間量。 有效率的控制器和驅動程式將使用較少的授權時間，留下較多的處理時間供使用者應用程式使用，同時增加整體的處理能力。  
  
-   **Processor: %User Time**  
  
     相當於處理器花費在執行使用者處理序 (如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) 的時間百分比。  
  
-   **系統：Processor Queue Length**  
  
     相當於等候處理器時間的執行緒數目。 當處理序的執行緒所需的處理器循環超過可用數量時，就會形成處理器瓶頸。 如果會有許多處理序嘗試利用處理器時間，您可能必須安裝更快的處理器。 或者，如果使用多處理器系統，則可以增加一個處理器。  
  
 在檢查處理器使用量時，請考慮 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體所執行的工作類型。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 正在執行許多計算，例如牽涉到彙總的查詢，或不需要磁碟 I/O 的記憶體繫結查詢 (Memory-bound Query) 時，就可以使用 100 % 的處理器時間。 如果這導致其他應用程式的效能降低，請變更工作負載。 例如，讓此電腦專門用來執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體。  
  
 正在處理許多用戶端要求而使用率約達 100% 時，可能代表佇列中已有處理序在等候處理器時間，而造成瓶頸。 增加更快的處理器可解決這個問題。  
  
  
