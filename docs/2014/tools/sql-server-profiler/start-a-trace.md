---
title: 啟動追蹤 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Profiler, stopping traces
- pausing traces
- Profiler [SQL Server Profiler], stopping traces
- Profiler [SQL Server Profiler], starting traces
- traces [SQL Server], starting
- SQL Server Profiler, pausing traces
- traces [SQL Server], stopping
- Profiler [SQL Server Profiler], pausing traces
- traces [SQL Server], pausing
- SQL Server Profiler, starting traces
- stopping traces
- starting traces
ms.assetid: aeeb38eb-229a-4c8b-ad66-57e9ce45fb6a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4b32b1d1d6416c6a8c6097a79dcba18eb62a89d8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48140241"
---
# <a name="start-a-trace"></a>啟動追蹤
  在您使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]來定義新追蹤或建立範本之後，即可使用新的追蹤定義或範本來啟動、暫停或停止擷取資料。  
  
## <a name="starting-a-trace"></a>啟動追蹤  
 當您啟動追蹤，而且所定義的來源是 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的執行個體時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 便會建立一個佇列，以提供暫存空間來放置所擷取的伺服器事件。  
  
 當您使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 來存取 SQL 追蹤時，啟動追蹤時就會開啟新的追蹤視窗 (如果尚未開啟)，並立即擷取資料。  
  
 當您使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 系統預存程序來存取 SQL 追蹤時，您必須在每次啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體時啟動追蹤，以便擷取資料。 啟動追蹤後，您只能修改追蹤的名稱。  
  
> [!NOTE]  
>  使用現有的追蹤時，您可以檢視屬性，但是不能修改屬性。 若要修改屬性，請停止或暫停追蹤。  
  
## <a name="see-also"></a>另請參閱  
 [連接到伺服器之後，自動啟動追蹤&#40;SQL Server Profiler&#41;](start-a-trace-automatically-after-connecting-to-a-server-sql-server-profiler.md)   
 [暫停追蹤 &#40;SQL Server Profiler&#41;](pause-a-trace-sql-server-profiler.md)   
 [停止追蹤 &#40;SQL Server Profiler&#41;](stop-a-trace-sql-server-profiler.md)   
 [清除追蹤視窗 &#40;SQL Server Profiler&#41;](clear-a-trace-window-sql-server-profiler.md)   
 [在追蹤暫停或停止之後執行追蹤 &#40;SQL Server Profiler&#41;](run-a-trace-after-it-has-been-paused-or-stopped-sql-server-profiler.md)  
  
  
