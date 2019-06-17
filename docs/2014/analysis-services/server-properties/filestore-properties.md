---
title: Filestore 屬性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Income property
- InitialBonus property
- PercentScanPerPrice property
- FileStore properties
- BackgroundTrimCost property
- Tax property
- PerformanceTrace property
- MinimumBalance property
- UnbufferedThreshold property
- BackgroundTrimAmount property
- MaximumBalance property
- MemoryLimitMin property
- MemoryLimit property
ms.assetid: 580cf0aa-7425-4d48-aa8d-128f5b488fcd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fe11b7a9cda6b3e75cb97faa17a381e2b0ea1afe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66069091"
---
# <a name="filestore-properties"></a>FileStore 屬性
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支援下表列出的 Filestore 伺服器屬性。 這些全部都是進階屬性，除非是在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援人員的指導之下，否則不應隨意變更。 如需有關其他伺服器屬性及如何設定伺服器屬性的詳細資訊，請參閱＜ [Configure Server Properties in Analysis Services](server-properties-in-analysis-services.md)＞。  
  
 **適用於：** 多維度與表格式伺服器模式  
  
## <a name="properties"></a>屬性  
 `MemoryLimit`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `MemoryLimitMin`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `PercentScanPerPrice`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `PerformanceTrace`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `RandomFileAccessMode`  
 此為布林屬性，指出是否在隨機檔案存取模式下存取資料庫檔案和快取檔案。 此屬性預設為關閉。 Analysis Services 在開啟分割資料檔進行讀取時，預設不會設定隨機檔案存取旗標。  
  
 在高階系統上，尤其是具有大型記憶體資源和多個 NUMA 節點的系統，使用隨機檔案存取會很有幫助。 在隨機存取模式下，Windows 會略過將資料從磁碟讀入系統檔案快取的頁面對應作業，藉此降低快取的競爭情況。  
  
 您將需要執行比較測試，判斷變更此屬性是否使查詢效能獲得改善。 如需執行比較測試的最佳作法，包括清除快取和避免常見的錯誤，請參閱 [SQL Server 2008 R2 Analysis Services 作業指南](https://go.microsoft.com/fwlink/?LinkID=225539)。 使用此屬性的權衡取捨的其他資訊，請參閱[ https://support.microsoft.com/kb/2549369 ](https://support.microsoft.com/kb/2549369)。  
  
 若要在 Management Studio 中檢視或修改這個屬性，請在伺服器屬性頁面中啟用進階屬性清單。 您也可以變更 msmdsrv.ini 檔案中的屬性。 設定這個屬性之後，建議重新啟動伺服器，否則會繼續在之前的模式下存取已開啟的檔案。  
  
 `UnbufferedThreshold`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
## <a name="memory-model-category"></a>記憶體模型類別目錄  
 `MemoryModel\Tax`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `MemoryModel\Income`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `MemoryModel\MaximumBalance`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `MemoryModel\MinimumBalance`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `MemoryModel\InitialBonus`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 中設定伺服器屬性](server-properties-in-analysis-services.md)   
 [判斷 Analysis Services 執行個體的伺服器模式](../instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
