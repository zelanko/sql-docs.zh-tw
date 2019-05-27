---
title: 執行緒集區屬性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- PriorityRatio property
- threads [Analysis Services]
- MinThreads property
- NumThreads property
- MaxThreads property
- Concurrency property
ms.assetid: e2697bb6-6d3f-4621-b9fd-575ac39c2185
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1fe324da14460d69d6930bf9d398a50e816f676f
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66068840"
---
# <a name="thread-pool-properties"></a>執行緒集區屬性
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 為許多作業使用多執行緒處理，透過平行執行多個作業改善整體伺服器效能。 為了更有效率地管理執行緒， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 使用執行緒集區預先配置執行緒，以使下一個作業有可用的執行緒。  
  
 每個 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體各自維護一組執行緒集區。 表格式執行個體和多維度執行個體使用執行緒集區的方式大不相同。 最重要的差異是只有多維度方案使用`IOProcess`執行緒集區。 因此，本主題中描述的 `PerNumaNode` 屬性，對表格式執行個體沒有意義。  
  
 本主題包含下列幾節：  
  
-   [Analysis Services 的執行緒管理](#bkmk_threadarch)  
  
-   [執行緒集區屬性參考](#bkmk_propref)  
  
-   [設定 GroupAffinity 將執行緒相似化為處理器群組中的處理器](#bkmk_groupaffinity)  
  
-   [設定 PerNumaNode 將 IO 執行緒相似化為 NUMA 節點中的處理器](#bkmk_pernumanode)  
  
-   [判斷目前的執行緒集區設定](#bkmk_currentsettings)  
  
-   [相依或相關屬性](#bkmk_related)  
  
-   [關於 MSMDSRV.INI](#bkmk_msmdrsrvini)  
  
> [!NOTE]  
>  NUMA 系統上的表格式部署超出本主題的範圍。 雖然表格式方案可以在 NUMA 系統上成功部署，但是表格式模型使用之記憶體中資料庫技術的效能特性在高度向上延展的架構上成效有限。 如需詳細資訊，請參閱[Analysis Services 案例研究：在大規模商業解決方案中使用表格式模型](https://msdn.microsoft.com/library/dn751533.aspx)並[調整表格式解決方案的硬體](https://go.microsoft.com/fwlink/?LinkId=330359)。  
  
##  <a name="bkmk_threadarch"></a> Analysis Services 的執行緒管理  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 使用多執行緒處理，透過增加平行執行的工作數，利用可用的 CPU 資源。 儲存引擎是多執行緒。 在儲存引擎內執行的多執行緒作業範例包含平行處理物件、處理發送至儲存引擎的個別查詢，或傳回查詢所要求的資料值。 公式引擎由於其評估之計算的序列本質，是單一執行緒。 每個查詢主要會在單一執行緒上執行，並要求 (且通常需要等候) 儲存引擎傳回資料。 查詢執行緒的執行時間較長，並且僅在完成整個查詢之後釋出。  
  
 在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 及更新版本上， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 預設會使用所有可用的邏輯處理器，最多可在執行更高版本 Windows 和 SQL Server 的系統上有 640 個處理器。 在啟動時，會將 msmdsrv.exe 處理序指派給特定處理器群組，但是經過一段時間後，便可在任何處理器群組中的任何邏輯處理器上排程執行緒。  
  
 使用大量處理器的一個副作用是當查詢和處理負載擴展到大量處理器，且對共用資料結構的競爭增加時，效能有時可能會降低。 在使用 NUMA 架構的高階系統上，特別容易發生這個問題，但在相同硬體上執行多個資料密集應用程式的非 NUMA 系統上，也可能發生這個問題。  
  
 若要減少此問題，您可以設定 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 作業類型與一組特定的邏輯處理器之間的相似性。 `GroupAffinity` 屬性可讓您建立自訂相似性遮罩，指定哪個系統資源用於 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 所管理的每一個執行緒集區類型。  
  
 您可以在用於各種 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 工作負載的五個執行緒集區之一設定自訂相似性：  
  
-   **簡短剖析**  是適用於簡短要求的剖析集區。 大小符合單一網路訊息的要求視為簡短要求。  
  
-   **完整剖析**  是適用於大小不符合單一網路訊息之其他所有要求的剖析集區。  
  
    > [!NOTE]  
    >  您可以使用任何剖析集區中的執行緒來執行查詢。 快速執行的查詢 (例如快速探索或取消要求) 有時會立即執行，而不會排入查詢執行緒集區的佇列中。  
  
-   `Query` 是執行剖析執行緒集區所未處理的所有要求的執行緒集區。 此執行緒集區中的執行緒會執行所有類型的作業，例如探索、DAX、MDX、DMX 和 DDL 命令。  
  
-   `IOProcess` 用於與多維度引擎中的儲存引擎查詢相關聯的 IO 作業。 這些執行緒完成的工作預期不會相依於其他執行緒。 這些執行緒通常會掃描單一分割區區段，並對區段資料執行篩選和彙總。 `IOProcess` 執行緒是對 NUMA 硬體組態特別敏感。 因此，此執行緒集區具有`PerNumaNode`組態屬性，可用來微調效能，如有需要。  
  
-   `Process` 適用於較長持續時間儲存引擎工作，包括彙總、 索引和認可作業。 ROLAP 儲存模式也會使用處理執行緒集區中的執行緒。  
  
> [!NOTE]  
>  雖然 Msmdsrv.ini 有執行緒集區設定`VertiPaq`區段中， `VertiPaq` \\ `ThreadPool` \\ `GroupAffinity`並`ThreadPool` \\ `CPUs`此處特意不記載。 這些屬性目前無法作業，將保留供日後使用。  
  
 為了服務要求， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 可能會超過最大執行緒集區限制，並在需要額外的執行緒以執行工作時，要求這些執行緒。 不過，當執行緒完成執行其工作時，如果目前的執行緒計數大於上限，該執行緒會直接結束，而不會傳回執行緒集區。  
  
> [!NOTE]  
>  超過最大執行緒集區計數是一項保護措施，只有在發生特定死結狀況時才會起作用。 若要避免失控的執行緒建立超過上限，執行緒在達到這個上限之後會逐步 (在一小段延遲之後) 建立。 超過最大執行緒計數時，可能導致工作執行的速度變慢。 如果效能計數器顯示執行緒計數經常超出執行緒集區大小上限，可能就意味著執行緒集區大小過低而不足以應付系統所要求的並行程度。  
  
 根據預設，執行緒集區大小取決於 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]，並以核心數目為依據。 您可以在伺服器啟動之後檢查 msmdsrv.log 檔案，以觀察選取的預設值。 當您練習微調效能時，您可以選擇增加執行緒集區及其他屬性的大小，以提升查詢或處理效能。  
  
##  <a name="bkmk_propref"></a> 執行緒集區屬性參考  
 本節描述每個 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體之 msmdsrv.ini 檔案中的執行緒集區屬性。 這些屬性的子集也會出現在 SQL Server Management Studio 中。  
  
 屬性是依照字母順序列出。  
  
|名稱|類型|描述|預設|指引|  
|----------|----------|-----------------|-------------|--------------|  
|`IOProcess` \ `Concurrency`|double|此為雙精確度浮點數值，決定可以一次佇列之執行緒數目的設定目標演算法。|2.0|此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。<br /><br /> 並行可用來初始化執行緒集區，會透過 Windows 的 I/O 完成通訊埠來實作。 如需詳細資料，請參閱 [I/O 完成連接埠](https://msdn.microsoft.com/library/windows/desktop/aa365198\(v=vs.85\).aspx) 。<br /><br /> 僅適用於多維度模型。|  
|`IOProcess` \ `GroupAffinity`|string|對應至系統上之處理器群組的十六進位值陣列，可用來設定 IOProcess 執行緒集區中的執行緒與每個處理器群組中的邏輯處理器之相似性。|無|您可以使用此屬性來建立自訂相似性。 此屬性預設為空白。<br /><br /> 如需詳細資訊，請參閱＜ [設定 GroupAffinity 將執行緒相似化為處理器群組中的處理器](#bkmk_groupaffinity) ＞。<br /><br /> 僅適用於多維度模型。|  
|`IOProcess` \ `MaxThreads`|ssNoversion|此為帶正負號的 32 位元整數，指定要包含在執行緒集區中的執行緒數目上限。|0|0 表示由伺服器決定預設值。 根據預設，伺服器將此值設定為 64，或設定為邏輯處理器數目的 10 倍 (以較高者為準)。 例如，在具有超執行緒的 4 核心系統上，執行緒集區最多為 80 個執行緒。<br /><br /> 如果將此值設定為負值，則伺服器會將該值乘以邏輯處理器的數目。 例如，若在具有 32 個邏輯處理器的伺服器上設定為 -10，最大值是 320 個執行緒。<br /><br /> 最大值會根據您先前定義的任何自訂相似性遮罩而受限於可用的處理器。 例如，如果您已設定執行緒集區相似性使用 32 個處理器的其中 8 個，而您現在將 MaxThreads 設定為 -10，執行緒集區的上限就是 10 乘以 8，即 80 個執行緒。<br /><br /> 此執行緒集區屬性所使用的實際值會在服務啟動時寫入 msmdsrv 記錄檔。<br /><br /> 如需微調執行緒集區設定的詳細資訊，請參閱《 [Analysis Services 操作指南](https://msdn.microsoft.com/library/hh226085.aspx)》。<br /><br /> 僅適用於多維度模型。|  
|`IOProcess` \ `MinThreads`|ssNoversion|此為帶正負號的 32 位元整數，指定要預先配置在執行緒集區中的執行緒數目下限。|0|0 表示由伺服器決定預設值。 預設的最小值是 1。<br /><br /> 如果將此值設定為負值，則伺服器會將該值乘以邏輯處理器的數目。<br /><br /> 此執行緒集區屬性所使用的實際值會在服務啟動時寫入 msmdsrv 記錄檔。<br /><br /> 如需微調執行緒集區設定的詳細資訊，請參閱《 [Analysis Services 操作指南](https://msdn.microsoft.com/library/hh226085.aspx)》。<br /><br /> 僅適用於多維度模型。|  
|`IOProcess` \ `PerNumaNode`|ssNoversion|此為帶正負號的 32 位元整數，決定為 msmdsrv 處理序建立的執行緒集區數目。|-1|有效值為 -1、0、1、2。<br /><br /> -1 = 伺服器根據 NUMA 節點數目選取不同的 IO 執行緒集區策略。 在具有少於 4 個 NUMA 節點的系統上，伺服器行為與 0 相同 (為系統建立一個 IOProcess 執行緒集區)。 在具有 4 個 (含) 以上節點的系統上，其行為與 1 相同 (為每個節點建立 IOProcess 執行緒集區)。<br /><br /> 0 = 停用每個 NUMA 節點執行緒集區，因此只有一個 IOProcess 執行緒集區供 msmdsrv.exe 處理序使用。<br /><br /> 1 = 為每個 NUMA 節點啟用一個 IOProcess 執行緒集區。<br /><br /> 2 = 為每個邏輯處理器啟用一個 IOProcess 執行緒集區。 每個執行緒集區中的執行緒會相似化為邏輯處理器的 NUMA 節點，並將理想的處理器設為邏輯處理器。<br /><br /> 如需詳細資訊，請參閱＜ [設定 PerNumaNode 將 IO 執行緒相似化為 NUMA 節點中的處理器](#bkmk_pernumanode) ＞。<br /><br /> 僅適用於多維度模型。|  
|`IOProcess` \ `PriorityRatio`|ssNoversion|此為帶正負號的 32 位元整數，可用來確保偶爾執行較低優先權的執行緒，即使較高優先權的佇列不是空的。|2|此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。<br /><br /> 僅適用於多維度模型。|  
|`IOProcess` \ `StackSizeKB`|ssNoversion|此為帶正負號的 32 位元整數，可在執行緒執行時用於調整記憶體配置。|0|此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。<br /><br /> 僅適用於多維度模型。|  
|**剖析**  \ `Long` \ `Concurrency`|double|此為雙精確度浮點數值，決定可以一次佇列之執行緒數目的設定目標演算法。|2.0|此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。<br /><br /> 並行可用來初始化執行緒集區，會透過 Windows 的 I/O 完成通訊埠來實作。 如需詳細資料，請參閱 [I/O 完成連接埠](https://msdn.microsoft.com/library/windows/desktop/aa365198\(v=vs.85\).aspx) 。|  
|**剖析**  \ `Long` \ `GroupAffinity`|string|對應至系統上之處理器群組的十六進位值陣列，可用來設定剖析執行緒與每個處理器群組中的邏輯處理器之相似性。|無|您可以使用此屬性來建立自訂相似性。 此屬性預設為空白。<br /><br /> 如需詳細資訊，請參閱＜ [設定 GroupAffinity 將執行緒相似化為處理器群組中的處理器](#bkmk_groupaffinity) ＞。|  
|**剖析**  \ `Long` \ `NumThreads`|ssNoversion|此為帶正負號的 32 位元整數屬性，其中會定義可為冗長命令建立的執行緒數目。|0|0 表示由伺服器決定預設值。 預設行為是將 `NumThreads` 設定為絕對值 4，或設定為邏輯處理器數目的 2 倍 (以較高者為準)。<br /><br /> 如果將此值設定為負值，則伺服器會將該值乘以邏輯處理器的數目。 例如，若在具有 32 個邏輯處理器的伺服器上設定為 -10，最大值是 320 個執行緒。<br /><br /> 最大值會根據您先前定義的任何自訂相似性遮罩而受限於可用的處理器。 例如，如果您已設定執行緒集區相似性使用 32 個處理器的其中 8 個，而您現在將 NumThreads 設定為 -10，執行緒集區的上限就是 10 乘以 8，即 80 個執行緒。<br /><br /> 此執行緒集區屬性所使用的實際值會在服務啟動時寫入 msmdsrv 記錄檔。|  
|**剖析**  \ `Long` \ `PriorityRatio`|ssNoversion|此為帶正負號的 32 位元整數，可用來確保偶爾執行較低優先權的執行緒，即使較高優先權的佇列不是空的。|0|此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。|  
|**剖析**  \ `Long` \ `StackSizeKB`|ssNoversion|此為帶正負號的 32 位元整數，可在執行緒執行時用於調整記憶體配置。|0|此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。|  
|**剖析**  \ `Short` \ `Concurrency`|double|此為雙精確度浮點數值，決定可以一次佇列之執行緒數目的設定目標演算法。|2.0|此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。<br /><br /> 並行可用來初始化執行緒集區，會透過 Windows 的 I/O 完成通訊埠來實作。 如需詳細資料，請參閱 [I/O 完成連接埠](https://msdn.microsoft.com/library/windows/desktop/aa365198\(v=vs.85\).aspx) 。|  
|**剖析**  \ `Short` \ `GroupAffinity`|string|對應至系統上之處理器群組的十六進位值陣列，可用來設定剖析執行緒與每個處理器群組中的邏輯處理器之相似性。|無|您可以使用此屬性來建立自訂相似性。 此屬性預設為空白。<br /><br /> 如需詳細資訊，請參閱＜ [設定 GroupAffinity 將執行緒相似化為處理器群組中的處理器](#bkmk_groupaffinity) ＞。|  
|**剖析**  \ `Short` \ `NumThreads`|ssNoversion|此為帶正負號的 32 位元整數屬性，其中會定義可為簡短命令建立的執行緒數目。|0|0 表示由伺服器決定預設值。 預設行為是將 `NumThreads` 設定為絕對值 4，或設定為邏輯處理器數目的 2 倍 (以較高者為準)。<br /><br /> 如果將此值設定為負值，則伺服器會將該值乘以邏輯處理器的數目。 例如，若在具有 32 個邏輯處理器的伺服器上設定為 -10，最大值是 320 個執行緒。<br /><br /> 最大值會根據您先前定義的任何自訂相似性遮罩而受限於可用的處理器。 例如，如果您已設定執行緒集區相似性使用 32 個處理器的其中 8 個，而您現在將 NumThreads 設定為 -10，執行緒集區的上限就是 10 乘以 8，即 80 個執行緒。<br /><br /> 此執行緒集區屬性所使用的實際值會在服務啟動時寫入 msmdsrv 記錄檔。|  
|**剖析**  \ `Short` \ `PriorityRatio`|ssNoversion|此為帶正負號的 32 位元整數，可用來確保偶爾執行較低優先權的執行緒，即使較高優先權的佇列不是空的。|0|此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。|  
|**剖析**  \ `Short` \ `StackSizeKB`|ssNoversion|此為帶正負號的 32 位元整數，可在執行緒執行時用於調整記憶體配置。|64 * 邏輯處理器數目|此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。|  
|`Process` \ `Concurrency`|double|此為雙精確度浮點數值，決定可以一次佇列之執行緒數目的設定目標演算法。|2.0|此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。<br /><br /> 並行可用來初始化執行緒集區，會透過 Windows 的 I/O 完成通訊埠來實作。 如需詳細資料，請參閱 [I/O 完成連接埠](https://msdn.microsoft.com/library/windows/desktop/aa365198\(v=vs.85\).aspx) 。|  
|`Process` \ `GroupAffinity`|string|對應至系統上之處理器群組的十六進位值陣列，可用來設定處理執行緒與每個處理器群組中的邏輯處理器之相似性。|無|您可以使用此屬性來建立自訂相似性。 此屬性預設為空白。<br /><br /> 如需詳細資訊，請參閱＜ [設定 GroupAffinity 將執行緒相似化為處理器群組中的處理器](#bkmk_groupaffinity) ＞。|  
|`Process` \ `MaxThreads`|ssNoversion|此為帶正負號的 32 位元整數，指定要包含在執行緒集區中的執行緒數目上限。|0|0 表示由伺服器決定預設值。 伺服器預設會將此值設為 64 的絕對值或是邏輯處理器數目 (以較高者為準)。 例如，在啟用超執行緒的 64 核心系統上 (導致 128 個邏輯處理器)，執行緒集區最多為 128 個執行緒。<br /><br /> 如果將此值設定為負值，則伺服器會將該值乘以邏輯處理器的數目。 例如，若在具有 32 個邏輯處理器的伺服器上設定為 -10，最大值是 320 個執行緒。<br /><br /> 最大值會根據您先前定義的任何自訂相似性遮罩而受限於可用的處理器。 例如，如果您已設定執行緒集區相似性使用 32 個處理器的其中 8 個，而您現在將 MaxThreads 設定為 -10，執行緒集區的上限就是 10 乘以 8，即 80 個執行緒。<br /><br /> 此執行緒集區屬性所使用的實際值會在服務啟動時寫入 msmdsrv 記錄檔。<br /><br /> 如需微調執行緒集區設定的詳細資訊，請參閱《 [Analysis Services 操作指南](https://msdn.microsoft.com/library/hh226085.aspx)》。|  
|`Process` \ `MinThreads`|ssNoversion|此為帶正負號的 32 位元整數，指定要預先配置在執行緒集區中的執行緒數目下限。|0|0 表示由伺服器決定預設值。 預設的最小值是 1。<br /><br /> 如果將此值設定為負值，則伺服器會將該值乘以邏輯處理器的數目。<br /><br /> 此執行緒集區屬性所使用的實際值會在服務啟動時寫入 msmdsrv 記錄檔。<br /><br /> 如需微調執行緒集區設定的詳細資訊，請參閱《 [Analysis Services 操作指南](https://msdn.microsoft.com/library/hh226085.aspx)》。|  
|`Process` \ `PriorityRatio`|ssNoversion|此為帶正負號的 32 位元整數，可用來確保偶爾執行較低優先權的執行緒，即使較高優先權的佇列不是空的。|2|此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。|  
|`Process` \ `StackSizeKB`|ssNoversion|此為帶正負號的 32 位元整數，可在執行緒執行時用於調整記憶體配置。|0|此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。|  
|`Query`  \ `Concurrency`|double|此為雙精確度浮點數值，決定可以一次佇列之執行緒數目的設定目標演算法。|2.0|此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。<br /><br /> 並行可用來初始化執行緒集區，會透過 Windows 的 I/O 完成通訊埠來實作。 如需詳細資料，請參閱 [I/O 完成連接埠](https://msdn.microsoft.com/library/windows/desktop/aa365198\(v=vs.85\).aspx) 。|  
|`Query` \ `GroupAffinity`|string|對應至系統上之處理器群組的十六進位值陣列，可用來設定處理執行緒與每個處理器群組中的邏輯處理器之相似性。|無|您可以使用此屬性來建立自訂相似性。 此屬性預設為空白。<br /><br /> 如需詳細資訊，請參閱＜ [設定 GroupAffinity 將執行緒相似化為處理器群組中的處理器](#bkmk_groupaffinity) ＞。|  
|`Query`  \ `MaxThreads`|ssNoversion|此為帶正負號的 32 位元整數，指定要包含在執行緒集區中的執行緒數目上限。|0|0 表示由伺服器決定預設值。 根據預設，伺服器將此值設定為絕對值 10，或設定為邏輯處理器數目的 2 倍 (以較高者為準)。 例如，在具有超執行緒的 4 核心系統上，執行緒數上限為 16。<br /><br /> 如果將此值設定為負值，則伺服器會將該值乘以邏輯處理器的數目。 例如，若在具有 32 個邏輯處理器的伺服器上設定為 -10，最大值是 320 個執行緒。<br /><br /> 最大值會根據您先前定義的任何自訂相似性遮罩而受限於可用的處理器。 例如，如果您已設定執行緒集區相似性使用 32 個處理器的其中 8 個，而您現在將 MaxThreads 設定為 -10，執行緒集區的上限就是 10 乘以 8，即 80 個執行緒。<br /><br /> 此執行緒集區屬性所使用的實際值會在服務啟動時寫入 msmdsrv 記錄檔。<br /><br /> 如需微調執行緒集區設定的詳細資訊，請參閱《 [Analysis Services 操作指南](https://msdn.microsoft.com/library/hh226085.aspx)》。|  
|`Query` \ `MinThreads`|ssNoversion|此為帶正負號的 32 位元整數，指定要預先配置在執行緒集區中的執行緒數目下限。|0|0 表示由伺服器決定預設值。 預設的最小值是 1。<br /><br /> 如果將此值設定為負值，則伺服器會將該值乘以邏輯處理器的數目。<br /><br /> 此執行緒集區屬性所使用的實際值會在服務啟動時寫入 msmdsrv 記錄檔。<br /><br /> 如需微調執行緒集區設定的詳細資訊，請參閱《 [Analysis Services 操作指南](https://msdn.microsoft.com/library/hh226085.aspx)》。|  
|`Query` \ `PriorityRatio`|ssNoversion|此為帶正負號的 32 位元整數，可用來確保偶爾執行較低優先權的執行緒，即使較高優先權的佇列不是空的。|2|此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。|  
|`Query`  \ `StackSizeKB`|ssNoversion|此為帶正負號的 32 位元整數，可在執行緒執行時用於調整記憶體配置。|0|此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。|  
  
##  <a name="bkmk_groupaffinity"></a> 設定 GroupAffinity 將執行緒相似化為處理器群組中的處理器  
 `GroupAffinity` 是為了進階微調而提供。 您可以使用 `GroupAffinity` 屬性設定 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行緒集區和特定處理器之間的相似性；但是對於大多數安裝，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 可以使用所有可用的邏輯處理器時，執行效果最好。 因此，預設不會指定群組相似性。  
  
 如果效能測試指出需要 CPU 最佳化，您可以考慮較高層級的方法，例如使用 Windows Server 資源管理員設定邏輯處理器和伺服器處理序之間的相似性。 這種方式與定義個別執行緒集區的自訂相似性相比，可更容易進行實作與管理。  
  
 如果這個方法不夠完善，您可以定義執行緒集區的自訂相似性，達成更大的精確度。 大型多核心系統 (NUMA 或非 NUMA) 會因為執行緒集區分佈於太廣泛的處理器範圍而導致降低效能，因此在這些系統上比較可能建議自訂相似性設定。 雖然您可以在有少於 64 個邏輯處理器的系統上設定 `GroupAffinity`，但是成效極低，甚至可能會降低效能。  
  
> [!NOTE]  
>  `GroupAffinity` 是由限制 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 所使用之核心數目的版本所限制。 在啟動時，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會使用版本資訊和 `GroupAffinity` 屬性，來計算 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 管理之所有 5 個執行緒集區的相似性遮罩。 Standard Edition 最多可以使用 16 個核心。 如果您在具有超過 16 個核心的大型多核心系統上安裝 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Standard Edition， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 只會使用其中 16 個。 如果升級舊版的企業執行個體，您最多可以使用 20 個核心。 如需有關版本和授權的詳細資訊，請參閱 [SQL Server 2012 授權概觀](https://go.microsoft.com/fwlink/?LinkId=246061)。  
  
### <a name="syntax"></a>語法  
 此值為每個處理器群組的十六進位值，代表 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 配置執行緒給指定執行緒集區時，會先嘗試使用的邏輯處理器。  
  
 **邏輯處理器的位元遮罩**  
  
 在一個處理器群組中最多可以有 64 個邏輯處理器。 針對群組中執行緒集區使用 (或不使用) 的每個邏輯處理器，此位元遮罩是 1 (或 0)。 一旦您計算位元遮罩，即可計算十六進位值做為值`GroupAffinity`。  
  
 **多個處理器群組**  
  
 處理器群組會在系統啟動時決定。 `GroupAffinity` 接受以逗號分隔清單中的每個處理器群組的十六進位值。 提供多個處理器群組 (在更高階的系統上最多 10 個) 時，可以透過指定 0x0 略過個別群組。 例如，在具有四個處理器群組 (0、1、2、3) 的系統上，可以透過為第一個和第三個值輸入 0x0，排除群組 0 和 2。  
  
 `<GroupAffinity>0x0, 0xFF, 0x0, 0xFF</GroupAffinity>`  
  
### <a name="steps-for-computing-the-processor-affinity-mask"></a>計算處理器相似性遮罩的步驟  
 您可以設定`GroupAffinity`在 msmdsrv.ini 或在 SQL Server Management Studio 中的伺服器屬性頁面中。  
  
1.  **判斷處理器和處理器群組數目**  
  
     您可以 [從 winsysinternals 下載 Coreinfo 公用程式](https://technet.microsoft.com/sysinternals/cc835722.aspx)。  
  
     執行 **coreinfo** 即可從 Logical Processor to Group Map 區段取得這項資訊， 並為每個邏輯處理器分別產生一行。  
  
2.  處理器的排序 (由右至左)： `7654 3210`  
  
     這個範例只顯示 8 個處理器 (0 至 7)，不過，處理器群組最多可以有 64 個邏輯處理器，而且企業等級的 Windows Server 最多可以有 10 個處理器群組。  
  
3.  **針對您要使用的處理器群組計算位元遮罩**  
  
     `7654 3210`  
  
     根據您要排除或包含邏輯處理器，以 0 或 1 取代此數值。 在具有八個處理器的系統上，如果您想要針對 Analysis Services 使用處理器 7、6、5、4 和 1，您的計算方式可能會如下所示：  
  
     `1111 0010`  
  
4.  **將二進位數字轉換成十六進位值**  
  
     使用計算機或轉換工具將二進位數字轉換成對應的十六進位值。 在此範例中， `1111 0010` 會轉換成 `0xF2`。  
  
5.  **在 GroupAffinity 屬性中輸入十六進位值**  
  
     在 msmdsrv.ini 或 Management Studio 中的 [伺服器] 屬性頁面中，設定`GroupAffinity`中計算的值至步驟 4。  
  
> [!IMPORTANT]  
>  設定`GroupAffinity`是包含多個步驟的手動工作。 計算時`GroupAffinity`，仔細檢查您的計算。 雖然 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會在整個遮罩無效時傳回錯誤，但有效和無效設定的組合也會導致 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 忽略屬性。 例如，如果位元遮罩包含額外的值， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會忽略這項設定，並使用系統上的所有處理器， 當發生這個動作時並不會出現任何錯誤或警告來提醒您，但是您可以檢查 msmdsrv.log 檔案來了解實際上是如何設定相似性。  
  
##  <a name="bkmk_pernumanode"></a> 設定 PerNumaNode 將 IO 執行緒相似化為 NUMA 節點中的處理器  
 多維度 Analysis Services 執行個體，您可以設定`PerNumaNode`上`IOProcess`執行緒集區，以進一步最佳化執行緒排程和執行。 而`GroupAffinity`識別的一組邏輯處理器要用於指定的執行緒集區`PerNumaNode`則更進一步地指定是否要建立多個執行緒集區，進一步相似化到允許的邏輯處理器的一部分。  
  
> [!NOTE]  
>  在 Windows Server 2012 上，請使用工作管理員來檢視電腦上的 NUMA 節點數目。 在工作管理員的 [效能] 索引標籤上選取 **[CPU]** ，再以滑鼠右鍵按一下圖表區域來檢視 NUMA 節點。 或者也可以從 Windows Sysinternals [下載](https://technet.microsoft.com/sysinternals/cc835722.aspx) Coreinfo 公用程式並執行 `coreinfo -n` ，傳回每個節點中的 NUMA 節點與邏輯處理器。  
  
 有效值`PerNumaNode`會為-1、 0、 1、 2 中所述[執行緒集區屬性參考](#bkmk_propref)本主題中的區段。  
  
### <a name="default-recommended"></a>預設值 (建議)  
 在具有 NUMA 節點的系統上，我們建議您使用 PerNumaNode=-1 預設值，讓 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 根據節點計數調整執行緒集區數目和執行緒相似性。 如果系統有少於 4 個節點[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]實作所描述的行為`PerNumaNode`= 0，而`PerNumaNode`= 1 適用於具有 4 個或多個節點的系統。  
  
### <a name="choosing-a-value"></a>選擇值  
 您也可以覆寫預設值，使用另一個有效值。  
  
 **設定 PerNumaNode=0**  
  
 系統會忽略 NUMA 節點。 只有一個 IOProcess 執行緒集區，而且該執行緒集區中的所有執行緒都會相似化到所有邏輯處理器。 根據預設 (PerNumaNode=-1)，如果電腦的 NUMA 節點少於 4 個，這是作用的設定值。  
  
 ![Numa、 處理器和執行緒集區的對應關係](../media/ssas-threadpool-numaex0.PNG "Numa、 處理器和執行緒集區對應")  
  
 **設定 PerNumaNode=1**  
  
 系統會針對每個 NUMA 節點建立 IOProcess 執行緒集區。 使用個別的執行緒集區可改善對本機資源的協調存取，例如 NUMA 節點的本機快取。  
  
 ![Numa、 處理器和執行緒集區的對應關係](../media/ssas-threadpool-numaex1.PNG "Numa、 處理器和執行緒集區對應")  
  
 **設定 PerNumaNode=2**  
  
 這個設定適用於執行大量 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 工作負載的極高階系統。 此屬性會在其最細微的層級設定 IOProcess 執行緒集區相似性，並在邏輯處理器層級建立及關聯個別的執行緒集區。  
  
 在下列範例中，如果系統有 4 個 NUMA 節點及 32 個邏輯處理器，設定`PerNumaNode`為 2 會產生 32 個 IOProcess 執行緒集區。 前 8 個執行緒集區中的執行緒會相似化為 NUMA 節點 0 中的所有邏輯處理器，但會將理想的處理器設為 0、1、2，最多 7。 後 8 個執行緒集區會相似化為 NUMA 節點 1 中的所有邏輯處理器，並將理想的處理器設為 8、9、10，最多 15，依此類推。  
  
 ![Numa、 處理器和執行緒集區的對應關係](../media/ssas-threadpool-numaex2.PNG "Numa、 處理器和執行緒集區對應")  
  
 在此相似性層級，排程器一律會先嘗試使用偏好的 NUMA 節點中的理想邏輯處理器。 如果邏輯處理器無法使用，排程器會選擇相同節點或相同處理器群組 (如果沒有其他執行緒可用) 中的其他處理器。 如需詳細資訊和範例，請參閱 [Analysis Services 2012 Configuration settings (Wordpress Blog)](https://go.microsoft.com/fwlink/?LinkId=330387)(Analysis Services 2012 組態設定 (Wordpress 部落格))。  
  
###  <a name="bkmk_workdistrib"></a> IOProcess 執行緒中的工作分配  
 當您考慮是否要將設定`PerNumaNode`屬性，了解如何`IOProcess`會使用執行緒可協助您做出更明智的決定。  
  
 請記得，`IOProcess`用於與多維度引擎中的儲存引擎查詢相關聯的 IO 作業。  
  
 當掃描區段時，此引擎會識別區段所屬的分割區，並且嘗試將區段工作加入分割區所使用的執行緒集區佇列。 一般而言，屬於分割區的所有區段都會將其工作加入相同執行緒集區的佇列。 在 NUMA 系統上，這個行為特別有利，因為分割區的所有掃描都將使用在本機配置給該 NUMA 節點之檔案系統快取中的記憶體。  
  
 下列案例的建議調整有時可以改善 NUMA 系統的查詢效能：  
  
-   若為低度資料分割的量值群組 (例如，只有一個資料分割)，增加資料分割數目。 只使用一個資料分割會導致引擎永遠將工作排入一個執行緒集區 (執行緒集區 0) 的佇列。 加入更多分割區可讓引擎使用其他執行緒集區。  
  
     或者，如果您無法建立額外的磁碟分割，嘗試設定`PerNumaNode`= 0，這個方式可增加執行緒集區 0 可用的執行緒數目。  
  
-   對於區段掃描平均分配在多個資料分割，設定的資料庫`PerNumaNode`為 1 或 2 可以提升查詢效能因為這樣會增加整體數目`IOProcess`執行緒集區的系統使用。  
  
-   方案有多個資料分割，但只有一個進行重度掃描，請嘗試設定`PerNumaNode`= 0 並檢查是否可以改善效能。  
  
 雖然分割區和維度掃描都會使用`IOProcess`執行緒集區，但是維度掃描只使用執行緒集區 0。 這樣會導致該執行緒集區中的工作負載稍微分配不平均，但是不平衡的狀態應該是暫時性的，因為維度掃描通常會非常快速且不頻繁。  
  
> [!NOTE]  
>  當變更伺服器屬性時，請記得組態選項會套用到目前執行個體中執行的所有資料庫。 請選擇有利於最重要的資料庫或最大資料庫數目的設定。 您無法在資料庫層級設定處理器相似性，也無法設定個別分割區與特定處理器之間的相似性。  
  
 如需有關工作架構的詳細資訊，請參閱《 [SQL Server 2008 Analysis Services 效能指南](https://www.microsoft.com/download/details.aspx?id=17303)》的第 2.2 節。  
  
##  <a name="bkmk_related"></a> 相依或相關屬性  
 第 2.4 節所述[Analysis Services 作業指南](https://msdn.microsoft.com/library/hh226085.aspx)，如果您增加處理執行緒集區時，您應該確定`CoordinatorExecutionMode`設定，以及`CoordinatorQueryMaxThreads`設定具有值，可讓您充分利用增加的執行緒集區大小。  
  
 Analysis Services 使用協調器執行緒收集完成處理或查詢要求所需的資料。 此協調器會先針對必須處理的每個分割區分別佇列一項作業。 根據分割區中必須掃描的區段總數，每項作業會接著繼續將更多作業排入佇列。  
  
 `CoordinatorExecutionMode` 的預設值為 -4，表示每個核心最多 4 個平行作業，限制儲存引擎中 Subcube 要求可平行執行的協調者作業總數。  
  
 `CoordinatorQueryMaxThreads` 的預設值為 16，限制每個資料分割可平行執行的區段作業數目。  
  
##  <a name="bkmk_currentsettings"></a> 判斷目前的執行緒集區設定  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會在啟動每項服務時，將目前的執行緒集區設定輸出至 msmdsrv.log 檔案，這些設定包含最小和最大執行緒、處理器相似性遮罩及並行。  
  
 下列範例是記錄檔摘錄，在啟用超執行緒的 4 核心系統上，顯示 Query 執行緒集區的預設值 (MinThread=0、MaxThread=0、Concurrency=2)。 相似性遮罩為 0xFF，表示 8 個邏輯處理器。 請注意，遮罩前面會附加前置零。 您可以忽略前置零。  
  
 `"10/28/2013 9:20:52 AM) Message: The Query thread pool now has 1 minimum threads, 16 maximum threads, and a concurrency of 16.  Its thread pool affinity mask is 0x00000000000000ff. (Source: \\?\C:\Program Files\Microsoft SQL Server\MSAS11.MSSQLSERVER\OLAP\Log\msmdsrv.log, Type: 1, Category: 289, Event ID: 0x4121000A)"`  
  
 請注意，設定 **MinThread** 和 **MaxThread** 的演算法會合併系統組態，特別是處理器數目。 下列部落格文章提供深入了解如何計算值：[Analysis Services 2012 組態設定 （Wordpress 部落格）](https://go.microsoft.com/fwlink/?LinkId=330387)。 請注意，後續版本可能會調整這些設定和行為。  
  
 下列清單會針對不同處理器組合顯示其他相似性遮罩設定的範例：  
  
-   8 核心系統上的處理器 3-2-1-0 的相似性會產生這個位元遮罩：00001111 和十六進位值：0xF  
  
-   8 核心系統上的處理器 7-6-5-4 的相似性會產生這個位元遮罩：11110000 和十六進位值：0xF0  
  
-   8 核心系統上的處理器 5-4-3-2 的相似性會產生這個位元遮罩：00111100 和十六進位值：0x3C  
  
-   8 核心系統上的處理器 7-6-1-0 的相似性會產生這個位元遮罩：11000011 和十六進位值：0xC3  
  
 請注意，在具有多個處理器群組的系統上，每個群組會產生個別的相似性遮罩，並以逗號分隔清單來表示。  
  
##  <a name="bkmk_msmdrsrvini"></a> 關於 MSMDSRV.INI  
 msmdsrv.ini 檔案包含 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的組態設定，因此會影響在該執行個體上執行的所有資料庫。 使用伺服器組態屬性不能只最佳化一個資料庫的效能而排除所有其他資料庫。 不過，您可以安裝多個 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體，並將每個執行個體設定為使用一些屬性，好讓資料庫受益於共用類似的特性或工作負載。  
  
 所有伺服器組態屬性都會包含在 msmdsrv.ini 檔案中。 可能需要修改的屬性子集也會出現在 SSMS 等管理工具中。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]之表格式執行個體和多維度執行個體的 msmdsrv.ini 內容相同， 但某些設定僅適用於一個模式。 屬性參考文件中會註明這些依據伺服器模式的行為差異。  
  
> [!NOTE]  
>  如需有關如何設定屬性的指示，請參閱＜ [Configure Server Properties in Analysis Services](server-properties-in-analysis-services.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [關於處理序和執行緒](/windows/desktop/ProcThread/about-processes-and-threads)   
 [多個處理器](/windows/desktop/ProcThread/multiple-processors)   
 [處理器群組](/windows/desktop/ProcThread/processor-groups)   
 [SQL Server 2012 中 Analysis Services 執行緒集區的變更](https://blogs.msdn.com/b/psssql/archive/2012/01/31/analysis-services-thread-pool-changes-in-sql-server-2012.aspx)   
 [Analysis Services 2012 Configuration settings (Wordpress Blog)](https://go.microsoft.com/fwlink/?LinkId=330387)   
 [支援具有超過 64 個處理器的系統](https://msdn.microsoft.com/library/windows/hardware/gg463349.aspx)   
 [SQL Server 2008 R2 Analysis Services 作業指南](https://go.microsoft.com/fwlink/?LinkID=225539)  
  
  
