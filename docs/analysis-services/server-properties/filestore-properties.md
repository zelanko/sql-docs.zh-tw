---
title: Filestore 屬性 |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ''
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ec29a17677032a764ae4604368ccc8cec243c11c
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="filestore-properties"></a>FileStore 屬性
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支援下表列出的 Filestore 伺服器屬性。 這些全部都是進階屬性，除非是在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援人員的指導之下，否則不應隨意變更。 如需其他伺服器屬性以及如何設定伺服器屬性的詳細資訊，請參閱 [Analysis Services 中的伺服器屬性](../../analysis-services/server-properties/server-properties-in-analysis-services.md)。  
  
 **適用於：** 多維度與表格式伺服器模式  
  
## <a name="properties"></a>屬性  
 **MemoryLimit**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **MemoryLimitMin**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **PercentScanPerPrice**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **PerformanceTrace**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **RandomFileAccessMode**  
 此為布林屬性，指出是否在隨機檔案存取模式下存取資料庫檔案和快取檔案。 此屬性預設為關閉。 Analysis Services 在開啟分割資料檔進行讀取時，預設不會設定隨機檔案存取旗標。  
  
 在高階系統上，尤其是具有大型記憶體資源和多個 NUMA 節點的系統，使用隨機檔案存取會很有幫助。 在隨機存取模式下，Windows 會略過將資料從磁碟讀入系統檔案快取的頁面對應作業，藉此降低快取的競爭情況。  
  
 您將需要執行比較測試，判斷變更此屬性是否使查詢效能獲得改善。 如需執行比較測試的最佳作法，包括清除快取和避免常見的錯誤，請參閱 [SQL Server 2008 R2 Analysis Services 作業指南](http://go.microsoft.com/fwlink/?LinkID=225539)。 使用此屬性之權衡取捨其他資訊，請參閱[ http://support.microsoft.com/kb/2549369 ](http://support.microsoft.com/kb/2549369)。  
  
 若要在 Management Studio 中檢視或修改這個屬性，請在伺服器屬性頁面中啟用進階屬性清單。 您也可以變更 msmdsrv.ini 檔案中的屬性。 設定這個屬性之後，建議重新啟動伺服器，否則會繼續在之前的模式下存取已開啟的檔案。  
  
 **UnbufferedThreshold**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
## <a name="memory-model-category"></a>記憶體模型類別目錄  
 **MemoryModel\Tax**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **MemoryModel\Income**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **MemoryModel\MaximumBalance**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **MemoryModel\MinimumBalance**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **MemoryModel\InitialBonus**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 中的伺服器屬性](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [判斷 Analysis Services 執行個體的伺服器模式](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
