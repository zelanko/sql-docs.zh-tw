---
title: 隔離效能問題 | Microsoft Docs
description: 使用 SQL Server Profiler 和系統監視器來監視 Transact-SQL、應用程式的相關問題、硬體和系統的相關問題，並對其進行疑難排解。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- isolating performance problems [SQL Server]
- monitoring performance [SQL Server], isolating problems
- database monitoring [SQL Server], isolating problems
- tuning databases [SQL Server], isolating problems
- monitoring server performance [SQL Server], isolating problems
- database performance [SQL Server], isolating problems
- server performance [SQL Server], isolating problems
ms.assetid: 2eb425cb-9166-4027-ae08-c8fc2d236f44
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 59a452da4fa48d422855416d308383fceb126791
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/17/2020
ms.locfileid: "86457917"
---
# <a name="isolate-performance-problems"></a>隔離效能問題
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  通常，同時使用數種 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Microsoft Windows 工具來隔離資料庫效能問題，會比一次使用一種工具要更有效率。 例如，稱為 Showplan 的圖形「執行計畫」功能可協助您快速識別出單一查詢中的死結。 不過，如果同時使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 與 Windows 的監視功能，可以更容易辨識出其他效能問題。  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 可以用來監視和疑難排解 Transact-SQL 及應用程式的相關問題。 「系統監視器」可以用來監視硬體與其他跟系統相關的問題。  
  
 您可以監視下列範圍來進行問題的疑難排解：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預存程序或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的批次。  
  
-   使用者活動，例如封鎖的鎖定或死結。  
  
-   硬體活動，例如磁碟使用量。  
  
 問題涵蓋了：  
  
-   跟撰寫不正確的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式有關的應用程式開發錯誤。  
  
-   硬體錯誤，例如磁碟或網路相關錯誤。  
  
-   因資料庫設計不正確而造成的過度封鎖。  
  
## <a name="tools-for-common-performance-problems"></a>一般效能問題的工具  
 能謹慎選取要各個工具監視或微調的效能問題同樣很重要。 工具與公用程式會根據想要解決的效能問題類型而有所不同。  
  
 以下主題描述許多監視與微調工具以及這些工具可發現的問題。  
  
 [找出瓶頸](../../relational-databases/performance/identify-bottlenecks.md)  
  
 [監視記憶體使用量](../../relational-databases/performance-monitor/monitor-memory-usage.md)  
  
  
