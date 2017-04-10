---
title: "軟體 NUMA (SQL Server) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "11/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "NUMA"
  - "soft-NUMA"
helpviewer_keywords: 
  - "NUMA"
  - "非統一記憶體存取"
  - "軟體 NUMA"
ms.assetid: 1af22188-e08b-4c80-a27e-4ae6ed9ff969
caps.latest.revision: 53
author: "CarlRabeler"
ms.author: "carlrab"
manager: "jhubbard"
caps.handback.revision: 52
---
# 軟體 NUMA (SQL Server)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  現代處理器在每個插槽有許多核心。 每個插槽通常代表單一 NUMA 節點。 SQL Server 資料庫引擎資料分割將每個 NUMA 節點分為內部結構和資料分割服務執行緒。  只要有了在每個插槽都含有 10 個或更多核心的處理器，使用軟體 NUMA 分割硬體 NUMA 節點通常會增加延展性和效能。 在 SQL Server 2014 SP2 之前，以軟體為基礎的 NUMA (軟體式 NUMA) 會要求您編輯登錄來加入節點組態親和性遮罩，並且是從每一部電腦進行設定，而不是從每個執行個體設定。  只要有了 SQL Server 2014 SP2 和 SQL Server 2016，當 SQL Server 服務啟動時，軟體式 NUMA 會自動設定為資料庫執行個體層級。  
  
> [!NOTE]  
>  軟體 NUMA 不支援熱新增處理器。  
  
## <a name="automatic-soft-numa"></a>自動軟體 NUMA  
 只要有了 SQL Server 2016，每當資料庫引擎伺服器在啟動時於每個 NUMA 節點或通訊端偵測到超過 8 個實體核心，就會根據預設值自動建立軟體 NUMA 節點。 計算節點中的實體核心時，不會區分超執行緒處理器核心。  當偵測到每個通訊端的實體核心超過 8 個時，Database Engine 服務會建立 NUMA 節點，此節點在理想情況下會包含 8 個核心，但可以減少至每個節點 5 個或增加至最多 9 個邏輯核心。 硬體節點的大小可由 CPU 關連遮罩限制。 請參閱   
            [ALTER SERVER CONFIGURATION &amp;#40;Transact-SQL&amp;#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md)。 NUMA 節點數目將永遠不會超過支援的 NUMA 節點數目上限。  
  
 您可以搭配 SET SOFTNUMA 引數使用 [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md) 陳述式來停用或重新啟用軟體式 NUMA。 變更此設定值需要重新啟動資料庫引擎才會生效。  
  
 下圖顯示當 SQL Server 偵測到硬體 NUMA 節點在每個節點或通訊端有超過 8 個實體核心時，您會在 SQL Server 錯誤記錄檔中看到的軟體 NUMA 資訊類型。  


``2016-11-14 13:39:43.17 Server      SQL Server detected 2 sockets with 12 cores per socket and 24 logical processors per socket, 48 total logical processors; using 48 logical processors based on SQL Server licensing. This is an informational message; no user action is required.``  
  **``2016-11-14 13:39:43.35 Server      Automatic soft-NUMA was enabled because SQL Server has detected hardware NUMA nodes with greater than 8 physical cores.``**  
  ``2016-11-14 13:39:43.63 Server      Node configuration: node 0: CPU mask: 0x0000000000555555:0 Active CPU mask: 0x0000000000555555:0. This message provides a description of the NUMA configuration for this computer. This is an informational message only. No user action is required.``  
  ``2016-11-14 13:39:43.63 Server      Node configuration: node 1: CPU mask: 0x0000000000aaaaaa:0 Active CPU mask: 0x0000000000aaaaaa:0. This message provides a description of the NUMA configuration for this computer. This is an informational message only. No user action is required.``  
  ``2016-11-14 13:39:43.63 Server      Node configuration: node 2: CPU mask: 0x0000555555000000:0 Active CPU mask: 0x0000555555000000:0. This message provides a description of the NUMA configuration for this computer. This is an informational message only. No user action is required.``  
  ``2016-11-14 13:39:43.63 Server      Node configuration: node 3: CPU mask: 0x0000aaaaaa000000:0 Active CPU mask: 0x0000aaaaaa000000:0. This message provides a description of the NUMA configuration for this computer. This is an informational message only. No user action is required.``

  
## <a name="manual-soft-numa"></a>手動軟體 NUMA  
 若要手動設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用軟體 NUMA 的話，必須停用自動軟體 NUMA 並編輯登錄來加入節點組態相似性遮罩。 當使用此方法時，軟體 NUMA 遮罩可陳述為二進位、DWORD (十六進位或十進位) 或 QWORD (十六進位或十進位) 登錄項目。 若要設定超過前 32 個 CPU，請使用 QWORD 或 BINARY 登錄值 (在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以前的版本不能使用 QWORD 值。)在修改登錄之後，您必須重新啟動 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 軟體式 NUMA 組態才會生效。  
  
> [!TIP] CPU 編號從 0 開始。  

> [!WARNING] [!INCLUDE[ssNoteRegistry](../../includes/ssnoteregistry-md.md)]  
  
 請設想下列範例。 一部具有八個 CPU 的電腦沒有硬體 NUMA。 三個軟體 NUMA 節點已設定。   
            [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體 A 是設定成使用 CPU 0 到 3。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的第二個執行個體安裝及設定為使用 CPU 4 到 7。 此範例可以視覺化方式表示如下：  
  
 `CPUs          0  1  2  3  4  5  6  7`  
  
 `Soft-NUMA   <-N0--><-N1-><----N2---->`  
  
 `SQL Server  <instance A ><instance B>`  
  
 發生大量 I/O 的執行個體 A，現在有兩個 I/O 執行緒和一個延遲寫入器執行緒，而執行處理器密集作業的執行個體 B，只有一個 I/O 執行緒和一個延遲寫入器執行緒。 不同記憶體數量可指派給執行個體，但與硬體 NUMA 不同，它們都是從相同作業系統記憶體區塊接收記憶體，而沒有記憶體對處理器的相似性。  
  
 延遲寫入器執行緒會繫結至實體 NUMA 記憶體節點的 SQL OS 檢視。 因此，呈現為實體 NUMA 節點的任何硬體都將等於建立的延遲寫入器執行緒數目。 如需詳細資訊，請參閱   
            [How It Works: Soft NUMA, I/O Completion Thread, Lazy Writer Workers and Memory Nodes](http://blogs.msdn.com/b/psssql/archive/2010/04/02/how-it-works-soft-numa-i-o-completion-thread-lazy-writer-workers-and-memory-nodes.aspx)(運作方式：軟體式 NUMA、I/O 完成執行緒、延遲寫入器背景工作和記憶體節點)。  
  
> [!NOTE] 當您升級 [!INCLUDE[ssNoVersion] (../Token/ssNoVersion_md.md)] 執行個體時，不會複製**軟體 NUMA** 登錄機碼。  
  
### <a name="set-the-cpu-affinity-mask"></a>設定 CPU 相似性遮罩  
 對執行個體 A 執行下列陳述式，藉由設定 CPU 相似性遮罩來設定它使用 CPU 0、1、2 和 3：  
  
```  
ALTER SERVER CONFIGURATION   
SET PROCESS AFFINITY CPU=0 TO 3;  
```  
  
 對執行個體 B 執行下列陳述式，藉由設定 CPU 相似性遮罩來設定它使用 CPU 4、5、6 和 7：  
  
```  
ALTER SERVER CONFIGURATION   
SET PROCESS AFFINITY CPU=4 TO 7;  
```  
  
### <a name="map-soft-numa-nodes-to-cpus"></a>將軟體 NUMA 節點對應到 CPU  
 使用 [登錄編輯程式] (regedit.exe)，加入下列登錄機碼，以便將軟體 NUMA 節點 0 對應到 CPU 0 和 1、將軟體 NUMA 節點 1 對應到 CPU 2 和 3，並且將軟體 NUMA 節點 2 對應到 CPU 4、 5、6 和 7。  
  
> [!TIP] 若要指定 CPU 60 到 63，請使用 QWORD 值 F000000000000000 或 BINARY 值 1111000000000000000000000000000000000000000000000000000000000000。  
  
 下列範例假設您有 DL580 G9 伺服器。該伺服器的每個插槽 (共有 4 個插槽) 安裝有 18 顆核心，且每個插槽各位在其 K 群組中。 您可以建立類似下列的軟體 numa 組態 (每個節點 6 顆核心、每個群組 3 個節點、4 個群組)。  
  
|具有多個 K 群組的 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 伺服器範例|類型|值名稱|值資料|  
|-----------------------------------------------------------------------------------------------------------------|----------|----------------|----------------|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node0|DWORD|CPUMask|0x3F|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node0|DWORD|群組|0|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node1|DWORD|CPUMask|0x0fc0|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node1|DWORD|群組|0|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node2|DWORD|CPUMask|0x3f000|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node2|DWORD|群組|0|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node3|DWORD|CPUMask|0x3F|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node3|DWORD|群組|1|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node4|DWORD|CPUMask|0x0fc0|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node4|DWORD|群組|1|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node5|DWORD|CPUMask|0x3f000|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node5|DWORD|群組|1|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node6|DWORD|CPUMask|0x3F|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node6|DWORD|群組|2|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node7|DWORD|CPUMask|0x0fc0|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node7|DWORD|群組|2|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node8|DWORD|CPUMask|0x3f000|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node8|DWORD|群組|2|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node9|DWORD|CPUMask|0x3F|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node9|DWORD|群組|3|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node10|DWORD|CPUMask|0x0fc0|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node10|DWORD|群組|3|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node11|DWORD|CPUMask|0x3f000|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node11|DWORD|群組|3|  
  
## <a name="metadata"></a>中繼資料  
 您可以使用下列 DMV 以檢視的目前狀態和軟體 NUMA 組態。  
  
-   [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)︰顯示 SOFTNUMA 目前的值 (0 或 1)  
  
-   [sys.dm_os_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-nodes-transact-sql.md)︰每個 NUMA 節點的 node_state_desc 資料行將顯示節點是否由軟體式 NUMA 所建立。  
  
-   [sys.dm_os_sys_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)：softnuma 和 softnuma_desc 資料行會顯示組態值。  
  
> [!NOTE] 雖然您可以使用 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 檢視自動軟體式 NUMA 執行中的值，但您無法使用 **sp_configure** 變更其值。 您必須搭配 SET SOFTNUMA 引數使用 [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md) 陳述式。  
  
## <a name="see-also"></a>另請參閱  
 [將 TCP/IP 通訊埠對應到 NUMA 節點 &#40;SQL Server&#41;](../../database-engine/configure-windows/map-tcp-ip-ports-to-numa-nodes-sql-server.md)   
 [affinity mask 伺服器組態選項](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md)   
 [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md)  
  
  