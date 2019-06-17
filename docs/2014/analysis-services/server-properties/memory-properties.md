---
title: 記憶體屬性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- LowMemoryLimit property
- MinimumAllocatedMemory property
- MidMemoryPrice property
- MemoryHeapType property
- memory [Analysis Services]
- DefaultPagesCountToReuse property
- TotalMemoryLimit property
- SessionMemoryLimit property
- VirtualMemoryLimit property
- WaitCountIfHighMemory property
- HighMemoryPrice property
- HeapTypeForObjects property
ms.assetid: 085f5195-7b2c-411a-9813-0ff5c6066d13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a88e2c1508ec849437d90b3de7c66705299dafc1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66068887"
---
# <a name="memory-properties"></a>記憶體屬性
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支援下表列出的伺服器記憶體屬性。 如需設定這些屬性的指引，請參閱《 [SQL Server 2008 R2 Analysis Services 操作指南](https://go.microsoft.com/fwlink/?LinkID=225539)》。  
  
 1 - 100 之間的值代表 **實體記憶體總計** 或 **虛擬位址空間**的百分比，以較少者為準。 超過 100 的值代表記憶體限制 (位元組)。  
  
 **適用於：** 多維度與表格式伺服器模式，除非另有指示。  
  
## <a name="properties"></a>屬性  
 `LowMemoryLimit`  
 帶正負號的 64 位元雙精確度浮點數屬性，此屬性定義一個臨界值，低於此值即表示伺服器記憶體不足 (以總實體記憶體的百分比表示)。 達到此限制時，執行個體將會開始關閉到期的工作階段並卸載未使用的計算，藉以緩慢地將記憶體清出快取。 伺服器不會在低於此限制時釋出記憶體。 預設值 65，表示記憶體下限為實體記憶體或虛擬位址空間的 65%，以較少者為準。  
  
 `TotalMemoryLimit`  
 定義達到時的臨界值，讓伺服器更積極地取消配置記憶體。 預設值 80% 的實體記憶體或虛擬位址空間的 65%，以較少者為準。  
  
 請注意，`TotalMemoryLimit` 永遠必須小於 `HardMemoryLimit`  
  
 `HardMemoryLimit`  
 指定記憶體閾值，超過此閥值後，執行個體會積極地終止使用中的使用者工作階段以減少記憶體的使用量。 所有終止的工作階段都會收到一個因為記憶體不足的壓力而取消的錯誤。 預設值零 (0)，代表 `HardMemoryLimit` 會設定為 `TotalMemoryLimit` 和系統總實體記憶體之間的中間值；若系統的實體記憶體大於處理序的虛擬位址空間，則會改用虛擬位址空間來計算 `HardMemoryLimit`。  
  
 `VirtualMemoryLimit`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `VertiPaqPagingPolicy`  
 指定伺服器記憶體不足時的分頁行為。 下列是有效值：  
  
 零 (**0**) 會停用分頁。 如果記憶體不足，處理會失敗，且會出現記憶體不足的錯誤。 如果您停用分頁，就必須授與 Windows 權限給服務帳戶。 如需指示，請參閱[設定服務帳戶 &#40;Analysis Services&#41;](../instances/configure-service-accounts-analysis-services.md)。  
  
 **1** 是預設值。 此屬性允許使用作業系統分頁檔 (pagefile.sys)，在磁碟中分頁。  
  
 當 `VertiPaqPagingPolicy` 設為 1 時，處理比較不可能因為記憶體限制而失敗，因為伺服器將會嘗試使用您指定的方法，在磁碟中分頁。 設定 `VertiPaqPagingPolicy` 屬性並不能保證記憶體錯誤永遠不會發生。 在下列狀況下，記憶體不足錯誤仍然可能發生：  
  
-   記憶體不足以供所有字典使用。 處理期間，Analysis Services 會針對記憶體中的每個資料行鎖定字典，所有這些字典不可大於 `VertiPaqMemoryLimit` 的指定值。  
  
-   虛擬位址空間不足以容納處理序。  
  
 若要解決持續發生的記憶體不足錯誤，您可以嘗試重新設計模型，減少需要處理的資料量，或在電腦上加入更多的實體記憶體。  
  
 僅適用於表格式伺服器模式。  
  
 `VertiPaqMemoryLimit`  
 如果允許在磁碟中分頁，此使用會指定分頁開始的記憶體耗用量 (以總記憶體的百分比表示) 層級。 預設值是 60。 如果記憶體耗用量低於 60%，伺服器將不會磁碟中分頁。  
  
 此屬性相依於 `VertiPaqPagingPolicyProperty`，且必須設為 1，才會進行分頁。  
  
 僅適用於表格式伺服器模式。  
  
 `HighMemoryPrice`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `MemoryHeapType`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 僅適用於多維度伺服器模式。  
  
 `HeapTypeForObjects`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 僅適用於多維度伺服器模式。  
  
 `DefaultPagesCountToReuse`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `HandleIA64AlignmentFaults`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `MidMemoryPrice`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `MinimumAllocatedMemory`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `PreAllocate`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `SessionMemoryLimit`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `WaitCountIfHighMemory`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 中設定伺服器屬性](server-properties-in-analysis-services.md)   
 [判斷 Analysis Services 執行個體的伺服器模式](../instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
