---
title: Analysis Services 記憶體屬性 |Microsoft Docs
ms.date: 01/15/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 055b46ab1464f360cfb89f9bf4d42c0b8997f841
ms.sourcegitcommit: c6e71ed14198da67afd7ba722823b1af9b4f4e6f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/16/2019
ms.locfileid: "54327859"
---
# <a name="memory-properties"></a>記憶體屬性
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  Analysis Services 會預先配置適度在啟動時的記憶體數量，因此可以立即處理要求。 隨著查詢和處理工作負載的增加，會配置額外的記憶體。 
  
  指定組態設定，即可控制釋放記憶體的臨界值。 例如， **HardMemoryLimit** 設定可指定自行強加的記憶體不足狀況 (依預設，未啟用此臨界值)；其中，變得需要更多資源時，就會立即拒絕新的要求。

若要深入了解使用每個 SQL Server Analysis Services 執行個體版本的最大記憶體，請參閱[版本及支援的功能的 SQL Server](../../sql-server/editions-and-components-of-sql-server-2017.md#Cross-BoxScaleLimits)。
  
 除非另有指示，下列設定將套用至表格式和多維度伺服器。  
 
## <a name="default-memory-configuration"></a>預設記憶體組態

根據預設設定，每個 Analysis Services 執行個體配置少量 RAM (40 MB 到 50 MB) 在啟動時，即使執行個體處於閒置狀態。 

請記住，預設組態是根據執行個體而定。 如果您是在相同硬體上執行多個 Analysis Services 執行個體 (例如表格式和多維度執行個體)，則每個執行個體都會配置它自己的記憶體，而這與其他執行個體無關。

下表簡述更常用的記憶體設定 (參考一節中會有更詳細的資訊)。 只有當 Analysis Services 會競用記憶體與相同的伺服器上的其他應用程式，請設定這些設定：

設定 | 描述
--------|------------
LowMemoryLimit | 針對多維度執行個體，伺服器第一次開始釋出配置給不常使用物件之記憶體的較低臨界值。
VertiPaqMemoryLimit | 針對表格式執行個體，伺服器第一次開始釋出配置給不常使用物件之記憶體的較低臨界值。
TotalMemoryLimit | 較高臨界值，Analysis Services 在達到此臨界值時會開始更積極地釋出記憶體，以清出空間供執行中要求以及新高優先順序要求使用。 
HardMemoryLimit | Analysis Services 因記憶體壓力而立即開始拒絕要求的另一個臨界值。 
 
## <a name="property-reference"></a>屬性參考

除非另有指定，否則下列屬性會套用至表格式和多維度模式。

 1 - 100 之間的值代表 **實體記憶體總計** 或 **虛擬位址空間**的百分比，以較少者為準。 超過 100 的值代表記憶體限制 (位元組)。
  
 **LowMemoryLimit**  
 帶正負號的 64 位元雙精確度浮點數屬性，定義 Analysis Services 開始釋出記憶體供低優先順序的物件，例如不常使用的快取的第一個臨界值。 配置記憶體之後，伺服器就不會在低於此限制時釋出記憶體。 預設值 65，表示記憶體下限為實體記憶體或虛擬位址空間的 65%，以較少者為準。  
  
 **TotalMemoryLimit**  
 定義臨界值，並在達到此臨界值時，讓伺服器取消配置記憶體，以清出空間供其他要求使用。 達到此限制時，執行個體將會開始關閉到期的工作階段並卸載未使用的計算，藉以緩慢地將記憶體清出快取。 預設值 80% 的實體記憶體或虛擬位址空間的 65%，以較少者為準。 **TotalMemoryLimit**永遠必須小於**HardMemoryLimit**  
  
 **HardMemoryLimit**  
 指定記憶體閾值，超過此閥值後，執行個體會積極地終止使用中的使用者工作階段以減少記憶體的使用量。 所有終止的工作階段都會收到關於記憶體不足的壓力所取消的錯誤。 預設值零 (0)，代表 **HardMemoryLimit** 會設定為 **TotalMemoryLimit** 和系統總實體記憶體之間的中間值；若系統的實體記憶體大於處理序的虛擬位址空間，則會改用虛擬位址空間來計算 **HardMemoryLimit**。  

**QueryMemoryLimit**   
只有 azure Analysis Services。 進階的屬性，即可控制多少記憶體可供暫存結果查詢期間。 僅適用於 DAX 量值和查詢。 它並不考慮查詢所使用的一般記憶體配置。 指定以百分比為單位，預設值取決於您的計劃。 

|計畫  |預設  |
|---------|---------|
|D1     |   80      |
|所有其他的計劃     |    20     |

可以變更這個屬性。 指定將值設定為 0 表示沒有限制。

 **VirtualMemoryLimit**  
  此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **VertiPaqPagingPolicy**  
  僅針對表格式執行個體，指定伺服器記憶體不足時的分頁行為。 下列是有效值：  
  
設定  |描述  
---------|---------
**0**     |  （如 Azure Analysis Services 的預設值）停用分頁。 如果記憶體不足，處理會失敗，且會出現記憶體不足的錯誤。 如果您停用分頁，就必須授與 Windows 權限給服務帳戶。 如需指示，請參閱[設定服務帳戶 &#40;Analysis Services&#41;](../../analysis-services/instances/configure-service-accounts-analysis-services.md)。 
**1**     |  （SQL Server Analysis services 的預設值）這個屬性允許使用作業系統分頁檔 (pagefile.sys) 磁碟中分頁。   
  
設為 1 時，處理比較不可能因為記憶體限制而失敗，因為伺服器將會嘗試使用您指定的方法，在磁碟中分頁。 設定 **VertiPaqPagingPolicy** 屬性並不能保證記憶體錯誤永遠不會發生。 在下列狀況下，記憶體不足錯誤仍然可能發生：  
  
-   記憶體不足以供所有字典使用。 在處理期間，伺服器，請鎖定記憶體中的每個資料行字典，所有這些字典不可大於指定的值**VertiPaqMemoryLimit**。  
  
-   虛擬位址空間不足以容納處理序。  
  
 若要解決持續發生的記憶體不足錯誤，您可以嘗試重新設計模型，減少需要處理的資料量，或在電腦上加入更多的實體記憶體。  
  
 **VertiPaqMemoryLimit**  
 僅適用於表格式執行個體，如果允許在磁碟中分頁，此屬性會指定分頁開始的記憶體耗用量 (以總記憶體的百分比表示) 層級。 預設值是 60。 如果記憶體耗用量低於 60%，伺服器將不會磁碟中分頁。 此屬性相依於 **VertiPaqPagingPolicyProperty**，且必須設為 1，才會進行分頁。  
  
 **HighMemoryPrice**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **MemoryHeapType**  
  此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。 以下為 SQL Server 2016 SP1 和更新版 Analysis Services 中的有效值：
  
  設定 | 描述
--------|------------
**-1** | (預設值) Automatic。 引擎將決定要使用哪一個。
**1** | Analysis Services 堆積。
**2** | Windows LFH。
**5** | 混合式配置器。 此配置器會使用針對 Windows LFH \<= 16KB 的配置和 AS 堆積針對 > 16KB 的配置。 
**6** | Intel TBB 配置器。 適用於 SQL Server 2016 SP1 (和更新版) Analysis Services 中。
  
  
 **HeapTypeForObjects**  
  此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。 下列是有效值：
  
   設定 | 描述
--------|------------
**-1** | (預設值) Automatic。 引擎將決定要使用哪一個。
**0** | Windows LFH 堆積。
**1** | Analysis Services 位置配置器。
**3** | 每個物件都有自己的 Analysis Services 堆積。

 
 **DefaultPagesCountToReuse**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **HandleIA64AlignmentFaults**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **MidMemoryPrice**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **MinimumAllocatedMemory**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **PreAllocate**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **SessionMemoryLimit**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **WaitCountIfHighMemory**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 中的伺服器屬性](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [判斷 Analysis Services 執行個體的伺服器模式](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
