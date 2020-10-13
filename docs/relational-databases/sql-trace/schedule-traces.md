---
description: 排程追蹤
title: 排程追蹤 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- filters [SQL Server], events
- traces [SQL Server]
- traces [SQL Server], stopping
- events [SQL Server], filters
- scheduling traces [SQL Server]
- traces [SQL Server], scheduling
- stopping traces
ms.assetid: 620b79db-924b-4502-8af3-39efcfca245d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1f86e9cf97c82ead3059d846f9709aa7a0c87d99
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810809"
---
# <a name="schedule-traces"></a>排程追蹤
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]有兩個方法可以排程追蹤。 您可以：  
  
-   啟用追蹤停止時間。  
  
-   使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 來排程追蹤。  
  
## <a name="specifying-a-stop-time"></a>指定停止時間  
 如果使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序或 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]，您可以指定追蹤停止時間。 最初設定追蹤時，必須設定停止時間。  
  
## <a name="scheduling-traces-by-using-sql-server-agent"></a>使用 SQL Server Agent 來排程追蹤  
 排程追蹤最好的方法是利用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 啟動追蹤，然後使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序 **sp_trace_setstatus**或 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]指定追蹤停止時間。  
  
 **若要設定追蹤的結束時間篩選**  
  
 [根據事件結束時間篩選事件 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-based-on-the-event-end-time-sql-server-profiler.md)  
  
 [sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)  
  
## <a name="see-also"></a>另請參閱  
 [自動化管理工作 &#40;SQL Server Agent&#41;](../../ssms/agent/automated-administration-tasks-sql-server-agent.md)  
  
