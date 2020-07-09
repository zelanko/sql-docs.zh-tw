---
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
ms.openlocfilehash: bad2aedb9299eb53e4f98e62a5aa48158f9ec457
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85750946"
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
 [自動化管理工作 &#40;SQL Server Agent&#41;](https://msdn.microsoft.com/library/541ee5ac-2c9f-4b74-b4f0-13b7bd5920b0)  
  
  
