---
title: 追蹤和重新執行事件 |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: smo
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- replaying events
- traces [SMO]
- events [SMO], replaying
- events [SMO], tracing
ms.assetid: f41b3f85-2f6c-4c3e-9776-8c73d2cc7a53
caps.latest.revision: 21
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 514c1dd7bf0bd2d3e8708368391d61bc39c0ed62
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="tracing-and-replaying-events"></a>追蹤及重新執行事件
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  在 SMO 中，**追蹤**和**Replay**中的物件<xref:Microsoft.SqlServer.Management.Trace>命名空間提供以程式設計方式存取[!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)]功能，可用於監視執行個體的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]或[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。 您可以擷取每一個事件的相關資料，並將資料儲存至檔案或資料表，以供稍後分析。 例如，您可以監視實際環境，查看哪些程序由於執行速度過慢而妨礙效能。  
  
 **追蹤**和**Replay**物件會提供一組可用來執行個體上建立追蹤的物件[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 您可以從自己的應用程式中使用這些物件，以手動方式為 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 建立追蹤。 另外，SMO**追蹤**物件可以用來讀取 SQL 追蹤檔案和資料表所建立的監視[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]， [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，或 DTS 記錄。  
  
 SMO**追蹤**物件可讓您執行下列功能：  
  
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
  
 追蹤資料，從**追蹤**和**Replay**物件都可以使用 SMO 應用程式，或它使用可以手動檢查[SQL Server Profiler](../../../tools/sql-server-profiler/sql-server-profiler.md)。 追蹤資料也會與相容[SQL 追蹤](../../../relational-databases/sql-trace/sql-trace.md)預存程序也提供追蹤功能。  
  
 SMO 追蹤物件位於 <xref:Microsoft.SqlServer.Management.Trace> 命名空間內，該命名空間需要參考 Microsoft.SQLServer.ConnectionInfo.dll 檔。  
  
 **追蹤**和**Replay**物件需要[ServerConnection](https://msdn.microsoft.com/en-us/library/microsoft.sqlserver.management.common.serverconnection.aspx) <xref:Microsoft.SqlServer.Management.Smo.Server.%23ctor%2A>物件來建立與執行個體的連線[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 [ServerConnection](https://msdn.microsoft.com/en-us/library/microsoft.sqlserver.management.common.serverconnection.aspx)物件位於[Microsoft.SqlServer.Management.Common](https://msdn.microsoft.com/en-us/library/microsoft.sqlserver.management.common)命名空間，需要參考 Microsoft.SQLServer.ConnectionInfo.dll 檔。  
  
> [!NOTE]  
>  **追蹤**和**Replay** 64 位元平台上不支援物件。  
  
  
