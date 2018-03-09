---
title: "監視記憶體使用量 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- tuning databases [SQL Server], memory
- monitoring server performance [SQL Server], memory usage
- isolating memory [SQL Server]
- paging rate [SQL Server]
- memory [SQL Server], monitoring usage
- monitoring [SQL Server], memory usage
- low-memory conditions
- database monitoring [SQL Server], memory usage
- available memory [SQL Server]
- page faults [SQL Server]
- monitoring performance [SQL Server], memory usage
- server performance [SQL Server], memory
ms.assetid: 1aee3933-a11c-4b87-91b7-32f5ea38c87f
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 18061fa8a59ab5cd5d86a7505162e5148767b9c7
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="monitor-memory-usage"></a>監視記憶體使用量
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 定期監視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，以確認記憶體使用量是在正常範圍內。  
  
 若要監視低記憶體的狀況，請使用以下物件計數器：  
  
-   **Memory: Available Bytes**  
  
-   **Memory: Pages/sec**  
  
 **Available Bytes** 計數器代表目前有多少記憶體位元組可供處理序使用。 **Pages/sec** 計數器會顯示由於硬體分頁錯誤而自磁碟取出，或由於分頁錯誤而寫入磁碟，以釋出工作集內空間的分頁數。  
  
 若 **Available Bytes** 計數器的數值偏低，代表電腦整體地缺乏記憶體，或有某個應用程式沒有釋出記憶體。 **Pages/sec** 計數器數值過高可能代表過度分頁。 監視 **Memory: Page Faults/sec** 計數器可確認磁碟活動並非分頁所造成。  
  
 分頁率 (連同分頁錯誤) 低是正常的，即使有許多可用記憶體的電腦也是如此。 當「Microsoft Windows 虛擬記憶體管理員 (VMM)」修剪 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和其他處理序的工作集大小時，它會從這些處理序取得分頁。 此 VMM 活動會造成分頁錯誤。 若要判定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或其他處理序是否造成過度分頁，請監視 **處理序執行個體的** Process: Page Faults/sec [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 計數器。  
  
 如需有關解決過度分頁的詳細資訊，請參閱 Windows 作業系統文件。  
  
## <a name="isolating-memory-used-by-sql-server"></a>隔離 SQL Server 所使用的記憶體  
 根據預設， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會根據可用的系統資源，動態變更它的記憶體需求。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 需要更多記憶體，它將詢問作業系統以判斷是否有可用的實體記憶體，並使用可用的記憶體。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 並不需要目前配置給它的記憶體，它會釋出記憶體給作業系統。 不過，您可以使用 **minservermemory**和 **maxservermemory** 伺服器組態選項，覆寫選項以動態使用記憶體。 如需詳細資訊，請參閱＜ [伺服器記憶體選項](../../database-engine/configure-windows/server-memory-server-configuration-options.md)＞。  
  
 若要監視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所使用的記憶體數量，請檢查下列效能計數器：  
  
-   **Process: Working Set**  
  
-   **SQL Server: Buffer Manager: Buffer Cache Hit Ratio**  
  
-   **SQL Server: Buffer Manager: Database Pages**  
  
-   **SQL Server: Memory Manager: Total Server Memory (KB)**  
  
 **WorkingSet** 計數器顯示處理序使用的記憶體數量。 如果這個數字一直低於 **「最小伺服器記憶體」** 與 **「最大伺服器記憶體」** 伺服器選項設定的記憶體數量，則代表 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 設定的記憶體過多。  
  
 **Buffer Cache Hit Ratio** 計數器專供應用程式使用。 不過，其數值最好為 90% 或更高。 請持續增加記憶體，直到該數值持續大於 90%。 數值大於 90% 代表有超過 90% 的資料要求，可自資料快取中得到所需的資料。  
  
 若 **TotalServerMemory (KB)** 計數器和電腦中的實體記憶體數量相比一直很高，可能代表需要更多的記憶體。  
  
## <a name="determining-current-memory-allocation"></a>決定目前的記憶體配置  
 以下查詢會傳回目前配置之記憶體的相關資訊。  
  
```  
SELECT  
(physical_memory_in_use_kb/1024) AS Memory_usedby_Sqlserver_MB,  
(locked_page_allocations_kb/1024) AS Locked_pages_used_Sqlserver_MB,  
(total_virtual_address_space_kb/1024) AS Total_VAS_in_MB,  
process_physical_memory_low,  
process_virtual_memory_low  
FROM sys.dm_os_process_memory;  
```  
  
  
