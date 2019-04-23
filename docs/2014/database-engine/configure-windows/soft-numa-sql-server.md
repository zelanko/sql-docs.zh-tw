---
title: 設定 SQL Server 使用軟體 NUMA (SQL Server) |Microsoft Docs
ms.custom: ''
ms.date: 07/12/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- NUMA
- non-uniform memory access
ms.assetid: 1af22188-e08b-4c80-a27e-4ae6ed9ff969
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 6ad0e30c0db83daf7e0cae4f7353d1f0a96a96d9
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "59953824"
---
# <a name="configure-sql-server-to-use-soft-numa-sql-server"></a>設定 SQL Server 使用軟體 NUMA (SQL Server)
現代處理器在每個插槽有許多核心。 每個插槽通常代表單一 NUMA 節點。 SQL Server 資料庫引擎資料分割將每個 NUMA 節點分為內部結構和資料分割服務執行緒。 處理器包含 10 個或多個核心，每個通訊端，使用軟體 NUMA (軟體 NUMA) 將硬體 NUMA 節點通常會增加延展性和效能。   

> [!NOTE]
> 軟體 NUMA 不支援熱新增處理器。
  
## <a name="automatic-soft-numa"></a>自動軟體 NUMA
從 SQL Server 2014 Service Pack 2，每當資料庫引擎伺服器偵測到 8 個以上的實體處理器，在啟動時，軟體 NUMA 節點會自動建立如果啟用追蹤旗標 8079 作為啟動參數。 計算實體處理器時，超執行緒處理器核心不會計算的。 當偵測到的實體處理器的數目超過 8 個每個通訊端時，database engine 服務會建立在理想情況下包含 8 個核心，但可以減少至每個節點 5 個最多 9 個邏輯處理器的 NUMA 節點。 硬體節點的大小可由 CPU 關連遮罩限制。 NUMA 節點數目將永遠不會超過支援的 NUMA 節點數目上限。

不追蹤旗標預設會停用 NUMA。 您可以讓 NUMA 使用追蹤旗標 8079。 變更此設定值需要重新啟動資料庫引擎才會生效。

下圖顯示當 SQL Server 偵測到硬體 NUMA 節點有超過 8 個邏輯處理器，且已啟用追蹤旗標 8079，您會看到 SQL Server 錯誤記錄檔中的軟體 NUMA 資訊類型。

![ssNoVersion](./media/soft-numa-sql-server/soft-numa.PNG)

> [!NOTE]
> 此行為由引擎和追蹤旗標 8079 控制 SQL Server 2016 開始，沒有任何作用。

## <a name="manual-soft-numa"></a>手動軟體 NUMA
  
若要設定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]若要以手動方式使用軟體 NUMA，您必須編輯登錄來加入節點組態親和性遮罩。 軟體 NUMA 遮罩可陳述為二進位、DWORD (十六進位或十進位) 或 QWORD (十六進位或十進位) 登錄項目。 若要設定超過前 32 個 CPU，請使用 QWORD 或 BINARY 登錄值 (在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以前的版本不能使用 QWORD 值。)您必須重新啟動[!INCLUDE[ssDE](../../includes/ssde-md.md)]設定軟體 NUMA。  
  
> [!TIP]  
>  CPU 編號從 0 開始。  
  
 [!INCLUDE[ssNoteRegistry](../../includes/ssnoteregistry-md.md)]  
  
 請設想下列範例。 一部具有八個 CPU 的電腦沒有硬體 NUMA。 三個軟體 NUMA 節點已設定。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體 A 是設定成使用 CPU 0 到 3。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的第二個執行個體安裝及設定為使用 CPU 4 到 7。 此範例可以視覺化方式表示如下：  
  
 `CPUs          0  1  2  3  4  5  6  7`  
  
 `Soft-NUMA   <-N0--><-N1-><----N2---->`  
  
 `SQL Server  <instance A ><instance B>`  
  
 發生大量 I/O 的執行個體 A，現在有兩個 I/O 執行緒和一個延遲寫入器執行緒，而執行處理器密集作業的執行個體 B，只有一個 I/O 執行緒和一個延遲寫入器執行緒。 不同記憶體數量可指派給執行個體，但與硬體 NUMA 不同，它們都是從相同作業系統記憶體區塊接收記憶體，而沒有記憶體對處理器的相似性。  
  
 延遲寫入器執行緒會繫結至實體 NUMA 記憶體節點的 SQL OS 檢視。 因此，呈現為實體 NUMA 節點的任何硬體都將等於建立的延遲寫入器執行緒數目。 如需詳細資訊，請參閱 [How It Works:軟體式 NUMA、 I/O 完成執行緒、 延遲寫入器工作者和記憶體節點](https://blogs.msdn.com/b/psssql/archive/2010/04/02/how-it-works-soft-numa-i-o-completion-thread-lazy-writer-workers-and-memory-nodes.aspx)。  
  
> [!NOTE]  
>  當您升級 **執行個體時，不會複製** 軟體 NUMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登錄機碼。  
  
### <a name="set-the-cpu-affinity-mask"></a>設定 CPU 相似性遮罩  
  
1.  對執行個體 A 執行下列陳述式，藉由設定 CPU 相似性遮罩來設定它使用 CPU 0、1、2 和 3：  
  
    ```  
    ALTER SERVER CONFIGURATION   
    SET PROCESS AFFINITY CPU=0 TO 3;  
    ```  
  
2.  對執行個體 B 執行下列陳述式，藉由設定 CPU 相似性遮罩來設定它使用 CPU 4、5、6 和 7：  
  
    ```  
    ALTER SERVER CONFIGURATION   
    SET PROCESS AFFINITY CPU=4 TO 7;  
    ```  
  
### <a name="map-soft-numa-nodes-to-cpus"></a>將軟體 NUMA 節點對應到 CPU  
  
-   使用 [登錄編輯程式] (regedit.exe)，加入下列登錄機碼，以便將軟體 NUMA 節點 0 對應到 CPU 0 和 1、將軟體 NUMA 節點 1 對應到 CPU 2 和 3，並且將軟體 NUMA 節點 2 對應到 CPU 4、 5、6 和 7。  
  
     下列範例假設您有 DL580 G9 伺服器。該伺服器的每個插槽 (共有 4 個插槽) 安裝有 18 顆核心，且每個插槽各位在其 K 群組中。 您可以建立類似下列的軟體 numa 組態 (每個節點 6 顆核心、每個群組 3 個節點、4 個群組)。  
  
    |具有多個 K 群組的 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 伺服器範例|類型|值名稱|值資料|  
    |------------------------------------------------------------------------|----------|----------------|----------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node0|DWORD|CPUMask|0x3F|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node0|DWORD|群組|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node1|DWORD|CPUMask|0x0fc0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node1|DWORD|群組|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node2|DWORD|CPUMask|0x3f000|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node2|DWORD|群組|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node3|DWORD|CPUMask|0x3F|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node3|DWORD|群組|1|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node4|DWORD|CPUMask|0x0fc0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node4|DWORD|群組|1|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node5|DWORD|CPUMask|0x3f000|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node5|DWORD|群組|1|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node6|DWORD|CPUMask|0x3F|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node6|DWORD|群組|2|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node7|DWORD|CPUMask|0x0fc0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node7|DWORD|群組|2|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node8|DWORD|CPUMask|0x3f000|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node8|DWORD|群組|2|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node9|DWORD|CPUMask|0x3F|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node9|DWORD|群組|3|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node10|DWORD|CPUMask|0x0fc0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node10|DWORD|群組|3|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node11|DWORD|CPUMask|0x3f000|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node11|DWORD|群組|3|  
  
     其他範例：  
  
    |[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|類型|值名稱|值資料|  
    |---------------------------|----------|----------------|----------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node0|DWORD|CPUMask|0x03|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node0|DWORD|群組|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node1|DWORD|CPUMask|0x0c|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node1|DWORD|群組|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node2|DWORD|CPUMask|0xf0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node2|DWORD|群組|0|  
  
    > [!TIP]  
    >  若要指定 CPU 60 到 63，請使用 QWORD 值 F000000000000000 或 BINARY 值 1111000000000000000000000000000000000000000000000000000000000000。  
  
    |[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|類型|值名稱|值資料|  
    |---------------------------|----------|----------------|----------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\NodeConfiguration\Node0|DWORD|CPUMask|0x03|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\NodeConfiguration\Node0|DWORD|群組|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\NodeConfiguration\Node1|DWORD|CPUMask|0x0c|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\NodeConfiguration\Node1|DWORD|群組|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\NodeConfiguration\Node2|DWORD|CPUMask|0xf0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\NodeConfiguration\Node2|DWORD|群組|0|  
  
    |SQL Server 2008 R2|類型|值名稱|值資料|  
    |------------------------|----------|----------------|----------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node0|DWORD|CPUMask|0x03|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node0|DWORD|群組|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node1|DWORD|CPUMask|0x0c|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node1|DWORD|群組|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node2|DWORD|CPUMask|0xf0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node2|DWORD|群組|0|  
  
    |SQL Server 2008|類型|值名稱|值資料|  
    |---------------------|----------|----------------|----------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node0|DWORD|CPUMask|0x03|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node1|DWORD|CPUMask|0x0c|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node2|DWORD|CPUMask|0xf0|  
  
    |SQL Server 2005|類型|值名稱|值資料|  
    |---------------------|----------|----------------|----------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\90\NodeConfiguration\Node0|DWORD|CPUMask|0x03|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\90\NodeConfiguration\Node1|DWORD|CPUMask|0x0c|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\90\NodeConfiguration\Node2|DWORD|CPUMask|0xf0|  
  
## <a name="see-also"></a>另請參閱  
 [將 TCP/IP 通訊埠對應到 NUMA 節點 &#40;SQL Server&#41;](map-tcp-ip-ports-to-numa-nodes-sql-server.md)   
 [affinity mask 伺服器組態選項](affinity-mask-server-configuration-option.md)   
 [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-server-configuration-transact-sql)  
  
  
