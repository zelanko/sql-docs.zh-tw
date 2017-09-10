---
title: "處理資料 (SSAS 表格式) |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d88f2dc9-2933-4be5-9bf3-48ffbc2d0a1a
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6fc5d0e934ae7fe4d7f9a00594c2f1ffd21bda1c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="process-data-ssas-tabular"></a>處理資料 (SSAS 表格式)
  當您將資料匯入至快取模式的表格式模型時，您可以擷取該資料在匯入時的快照集。 在某些情況下，該資料可能永遠不會變更，因此不需要在模型中更新。 但是，您匯入的資料很有可能定期變更，因此為了讓模型可以反映資料來源的最新資料，您必須處理 (重新整理) 資料並重新計算導出資料。 若要更新模型中的資料，您可以在所有資料表上、在個別資料表上、透過資料分割或透過資料來源連接，來執行處理動作。  
  
 撰寫模型專案時，必須在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]手動起始處理動作。 部署模型之後，即可使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 執行處理作業或使用指令碼排程處理作業。 此處所述的工作都屬於您在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中製作模型期間可以執行的處理動作。 如需已部署模型之程序動作的詳細資訊，請參閱[處理資料庫、資料表或資料分割 &#40;Analysis Services&#41;](../../analysis-services/tabular-models/process-database-table-or-partition-analysis-services.md)。  
  
## <a name="related-tasks"></a>相關工作  
  
|主題|說明|  
|-----------|-----------------|  
|[手動處理資料 (SSAS 表格式)](../../analysis-services/tabular-models/manually-process-data-ssas-tabular.md)|描述如何手動處理模型工作空間資料。|  
|[疑難排解處理資料 (SSAS 表格式)](../../analysis-services/troubleshoot-process-data-ssas-tabular.md)|描述如何疑難排解處理作業。|  
  
  
