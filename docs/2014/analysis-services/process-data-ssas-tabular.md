---
title: 處理資料（SSAS 表格式） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: d88f2dc9-2933-4be5-9bf3-48ffbc2d0a1a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0a0ca45681866e0ba96edaa81c21445a89f94275
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66070694"
---
# <a name="process-data-ssas-tabular"></a>處理資料 (SSAS 表格式)
  當您將資料匯入至快取模式的表格式模型時，您可以擷取該資料在匯入時的快照集。 在某些情況下，該資料可能永遠不會變更，因此不需要在模型中更新。 但是，您匯入的資料很有可能定期變更，因此為了讓模型可以反映資料來源的最新資料，您必須處理 (重新整理) 資料並重新計算導出資料。 若要更新模型中的資料，您可以在所有資料表上、在個別資料表上、透過資料分割或透過資料來源連接，來執行處理動作。  
  
 撰寫模型專案時，必須在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]手動起始處理動作。 部署模型之後，即可使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 執行處理作業或使用指令碼排程處理作業。 此處所述的工作都屬於您在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中製作模型期間可以執行的處理動作。 如需已部署模型之處理動作的詳細資訊，請參閱[處理資料庫、資料表或資料分割](tabular-models/process-database-table-or-partition-analysis-services.md)。  
  
## <a name="related-tasks"></a>相關工作  
  
|主題|描述|  
|-----------|-----------------|  
|[手動處理 &#40;SSAS 表格式&#41;的資料](manually-process-data-ssas-tabular.md)|描述如何手動處理模型工作空間資料。|  
|[針對 &#40;SSAS 表格式&#41;處理資料進行疑難排解](troubleshoot-process-data-ssas-tabular.md)|描述如何疑難排解處理作業。|  
  
  
