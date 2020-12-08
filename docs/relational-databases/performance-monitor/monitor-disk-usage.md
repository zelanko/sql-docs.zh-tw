---
title: 監視磁碟使用量 | Microsoft Docs
description: 監視 SQL Server 的磁碟活動涉及監視磁碟 I/O 與偵測額外的分頁方式，以及隔離 SQL Server 建立的磁碟活動。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- database monitoring [SQL Server], disk usage
- disks [SQL Server]
- monitoring performance [SQL Server], disk usage
- server performance [SQL Server], disk usage
- monitoring [SQL Server], disk activity
- excess paging [SQL Server]
- tuning databases [SQL Server], disk usage
- I/O [SQL Server], monitoring
- disks [SQL Server], monitoring activity
- isolating disk activity [SQL Server]
- database performance [SQL Server], disk usage
- monitoring server performance [SQL Server], disk usage
ms.assetid: 1525449c-ea7d-4222-b294-1ba1fe99c9ac
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: de77b88d4b82e0fd7360e76d090dd13468ef2a53
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505972"
---
# <a name="monitor-disk-usage"></a>監視磁碟使用量
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會使用 Microsoft Windows 作業系統輸入/輸出 (I/O) 呼叫，在您的磁碟上執行讀取和寫入作業。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會管理何時及如何執行磁碟 I/O，但是 Windows 作業系統會執行基礎 I/O 作業。 I/O 子系統包含了系統匯流排、磁碟控制卡、磁碟、磁帶機、光碟機和許多其他的 I/O 裝置。 磁碟 I/O 經常是造成系統瓶頸的原因。  
  
 監視磁碟活動涉及兩個重點：  
  
-   監視磁碟 I/O 與偵測額外的分頁方式  
  
-   隔離 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 建立的磁碟活動  
  
 如需詳細資訊，請參閱[監視磁碟使用量](https://social.technet.microsoft.com/wiki/contents/articles/monitoring-disk-usage.aspx) \(英文\)。 
 
 如需如何針對 SQL Server 中的 I/O 問題進行疑難排解的詳細資訊，請參閱 [I/O 速度變慢 - SQL Server 和磁碟 I/O 效能](https://techcommunity.microsoft.com/t5/SQL-Server-Support/Slow-I-O-SQL-Server-and-disk-I-O-performance/ba-p/333983) \(英文\)。
  
  
