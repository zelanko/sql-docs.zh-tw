---
title: 追蹤和重新執行事件 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- replaying events
- traces [SMO]
- events [SMO], replaying
- events [SMO], tracing
ms.assetid: f41b3f85-2f6c-4c3e-9776-8c73d2cc7a53
author: stevestein
ms.author: sstein
ms.openlocfilehash: bd75fdae7fc871101aa07785561c8277783a424f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85063057"
---
# <a name="tracing-and-replaying-events"></a>追蹤及重新執行事件
  在 SMO 中，`Trace` 命名空間中的 `Replay` 和 <xref:Microsoft.SqlServer.Management.Trace> 物件會提供 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] 功能的程式設計存取方式，該功能是用來監視 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 的執行個體。 您可以擷取每一個事件的相關資料，並將資料儲存至檔案或資料表，以供稍後分析。 例如，您可以監視實際環境，查看哪些程序由於執行速度過慢而妨礙效能。  
  
  和  物件會提供一組物件，這一組物件可在  執行個體上用來建立追蹤。 您可以從自己的應用程式中使用這些物件，以手動方式為 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 建立追蹤。 另外，SMO `Trace` 物件也可用來讀取之前透過監視 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]、[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 或 DTS 記錄所建立的 SQL 追蹤檔案和資料表。  
  
 SMO `Trace` 物件可讓您執行下列功能：  
  
-   建立追蹤。  
  
-   設定追蹤的篩選。  
  
-   設定正在追蹤的事件。  
  
-   停止或啟動追蹤。  
  
-   讀取追蹤檔案和追蹤資料表。  
  
-   取得有關追蹤事件的資訊。  
  
-   取得有關追蹤篩選的資訊。  
  
-   以程式設計方式操作追蹤資料。  
  
-   撰寫追蹤資料表和追蹤檔案。  
  
-   重新執行追蹤檔案或追蹤資料表。  
  
 和物件中的追蹤 `Trace` 資料 `Replay` 可由 SMO 應用程式使用，也可以使用[SQL Server Profiler](../../../tools/sql-server-profiler/sql-server-profiler.md)以手動方式進行檢查。 追蹤資料也與也提供追蹤功能的[SQL 追蹤](../../sql-trace/sql-trace.md)預存程式相容。  
  
 SMO 追蹤物件位於 <xref:Microsoft.SqlServer.Management.Trace> 命名空間內，該命名空間需要參考 Microsoft.SQLServer.ConnectionInfo.dll 檔。  
  
 `Trace` 和 `Replay` 物件會要求 <xref:Microsoft.SqlServer.Management.Common.ServerConnection><xref:Microsoft.SqlServer.Management.Smo.Server.%23ctor%2A> 物件建立與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的連接。  物件位於  命名空間內，該命名空間需要參考 Microsoft.SQLServer.ConnectionInfo.dll 檔。  
  
> [!NOTE]  
>  64 位元平台上不支援 `Trace` 和 `Replay` 物件。  
  
  
