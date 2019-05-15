---
title: 建立排程並將排程附加至作業 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server]
- scheduling jobs [SQL Server]
- jobs [SQL Server], scheduling
- CPU [SQL Server], idle conditions
- automatic job processing
- SQL Server Agent jobs, scheduling
- idle time [SQL Server]
ms.assetid: 079c2984-0052-4a37-a2b8-4ece56e6b6b5
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: b4df842e4d9df51fb11f195a6c693700697407bd
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2019
ms.locfileid: "65096879"
---
# <a name="create-and-attach-schedules-to-jobs"></a>建立及附加排程至作業
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

排程 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業是表示定義在沒有使用者互動的情況下讓作業開始執行的條件。 您可以透過建立作業的新排程，或將現有的排程附加至作業，將作業排程為自動執行。  
  
建立排程的方式有兩種：  
  
-   在您建立作業時建立排程。  
  
-   在 [物件總管] 中建立排程。  
  
建立排程之後，您就可以將該排程附加至多個作業，即使排程是針對特定作業所建立的也一樣。 此外，您也可以從作業中卸離排程。  
  
排程可以依據時間或事件。 例如，您可以將作業排程為在下列時間執行：  
  
-   每當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 啟動時。  
  
-   每當電腦的 CPU 使用率達到您定義為閒置的等級時。  
  
-   某個特定的日期和時間。  
  
-   執行循環排程時。  
  
除了作業排程之外，您也可以建立警示，讓它藉由執行作業而回應事件。  
  
> [!NOTE]  
> 一次只能執行該作業的一個執行個體。 若您在一項作業依排程執行時又以手動操作來執行， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 會拒絕該要求。  
  
若要防止排程的作業執行，您必須進行下列其中一項動作：  
  
-   停用排程。  
  
-   停用作業。  
  
-   從作業中卸離排程。  
  
-   停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務。  
  
-   刪除排程。  
  
即使排程未啟動，當回應警示或使用者手動執行作業時，作業仍會回應。 若未啟用作業排程，則所有使用該排程的作業都不會啟用該排程。  
  
您必須明確地重新啟用已停用排程。 編輯排程並不會自動重新啟用排程。  
  
## <a name="scheduling-start-dates"></a>排程開始日期  
排程的開始日期必須大於或等於 19900101。  
  
當您要將排程附加至作業時，應該檢閱此排程用來首次執行作業的開始日期。 此開始日期會取決於您將排程附加至作業的日期和時間。 例如，您可以建立在隔週星期一上午 8:00 執行的排程。 如果您在 2008 年 3 月 3 日星期一上午 10:00 建立某個作業，排程開始日期就是 2008 年 3 月 17 日星期一。 如果您在 2008 年 3 月 4 日星期二建立另一個作業，排程開始日期就是 2008 年 3 月 10 日星期一。  
  
當您將排程附加至作業之後，可以變更排程開始日期。  
  
## <a name="cpu-idle-schedules"></a>CPU 閒置排程  
為最大化 CPU 資源，您可以為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 定義 CPU 閒置條件。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 使用 CPU 閒置條件設定來判斷執行作業的最佳時間。 例如，您可以將重建索引作業排程在 CPU 閒置時間與慢速實際執行期間發生。  
  
定義作業在 CPU 閒置時間執行之前，請先判斷正常處理時的 CPU 負載。 如果要判斷負載，請使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 或效能監視器來監視伺服器流量並收集統計資料。 您可以使用所收集的資訊來設定 CPU 閒置時間百分比與期間。  
  
定義 CPU 閒置條件時，請以低於正常 CPU 使用量 (在指定時間) 的百分比來指定。 接著，設定時間量。 當 CPU 使用量在指定的時間內低於指定的百分比時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 會啟動所有具有 CPU 閒置時間排程的作業。 如需使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 或「效能監視器」來監視 CPU 使用量的詳細資訊，請參閱 [監視 CPU 使用量](../../relational-databases/performance-monitor/monitor-cpu-usage.md)。  
  
## <a name="related-tasks"></a>相關工作  
  
|||  
|-|-|  
|**說明**|**主題**|  
|描述如何建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業的排程。|[Create a Schedule](../../ssms/agent/create-a-schedule.md)|  
|描述如何排程 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業。|[排程作業](../../ssms/agent/schedule-a-job.md)|  
|說明如何定義伺服器的 CPU 閒置條件。|[設定 CPU 閒置與持續時間 &#40;SQL Server Management Studio&#41;](../../ssms/agent/set-cpu-idle-time-and-duration-sql-server-management-studio.md)|  
  
## <a name="see-also"></a>另請參閱  
[sp_help_jobschedule](../../relational-databases/system-stored-procedures/sp-help-jobschedule-transact-sql.md)  
[sysjobschedules](../../relational-databases/system-tables/dbo-sysjobschedules-transact-sql.md)  
  
