---
title: 建立追蹤與 Windows 效能記錄資料的關聯 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- correlating trace with log data
- logs [SQL Server], traces
- Profiler [SQL Server Profiler], correlating trace with log data
- traces [SQL Server], logs
- SQL Server Profiler, correlating trace with log data
ms.assetid: 1e4412c8-d27c-4aae-9b35-214128d1d00a
author: stevestein
ms.author: sstein
ms.openlocfilehash: 879441c948f0ad04b971159a37ec0dcec90e3ada
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85064051"
---
# <a name="correlate-a-trace-with-windows-performance-log-data"></a>使追蹤與 Windows 效能記錄資料相互關聯
  使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]，您可以開啟 Microsoft Windows 效能記錄，選擇要與追蹤相互關連的計數器，而且在 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 圖形化使用者介面中，讓選取的效能計數器顯示在追蹤的旁邊。 選取追蹤視窗中的事件後， [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 的 [系統監視器] 資料窗格中的紅色直條，表示與選取的追蹤事件相互關聯的效能記錄資料。  
  
 若要使追蹤與效能計數器相互關聯，請開啟包含 [StartTime]  與 [EndTime]  資料行的追蹤檔案或資料表，然後在  **[檔案]** [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 功能表上，按一下 [匯入效能資料]  。 接著可以開啟效能記錄，然後選取要與追蹤相互關聯的「系統監視器」物件與計數器。  
  
## <a name="see-also"></a>另請參閱  
 [使追蹤與 Windows 效能記錄資料產生相互關聯 &#40;SQL Server Profiler&#41;](correlate-a-trace-with-windows-performance-log-data.md)  
  
  
