---
title: 資料分割 (SSAS 表格式) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 708b9bdf-8c0b-4476-809a-8f616be23a58
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8126278319caff77a3d4ff6a334ed985c190288e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62795495"
---
# <a name="partitions-ssas-tabular"></a>分割區 (SSAS 表格式)
  分割區會將一個資料表分割成多個邏輯部分。 接著，每個分割區可以不受其他分割區的影響，單獨處理 (重新整理)。 在模型製作期間，使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 的 [分割區] 對話方塊建立的分割區，會套用至模型工作空間資料庫。 部署模型之後，為模型工作空間資料庫定義的分割區，會複製到已部署的模型資料庫中。 您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的 [分割區] 對話方塊，為已部署的模型資料庫進一步建立及管理分割區。  此主題中提供的資訊描述在模型製作期間，使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]的 [分割區管理員] 對話方塊建立的分割區。 如需為已部署的模型建立及管理資料分割的相關資訊，請參閱[建立及管理表格式模型資料分割 &#40;SSAS 表格式&#41;](create-and-manage-tabular-model-partitions-ssas-tabular.md)。  
  
 本主題的章節：  
  
-   [優點](#bkmk_benefits)  
  
-   [相關工作](#bkmk_related_tasks)  
  
##  <a name="bkmk_benefits"></a> 優點  
 表格式模型中的分割區，會將一個資料表分割成多個邏輯分割區物件。 接著，每個資料分割可以不受其他資料分割的影響，單獨進行處理。 例如，資料表的其中一些資料列集可能包含不常變更的資料，而其他一些資料列集則包含經常變更的資料。 在此情況下，如果您只想處理部分資料，則不需要處理所有資料。 分割區可讓您將需要經常處理的資料部分，與不常處理的資料加以分割。  
  
 有效的模型設計能善加利用分割區，以避免不必要的處理及 Analysis Services 伺服器上之後續處理器的負載，同時，還可確保資料的處理和重新整理頻率能反映資料來源的最新資料。 您在模型製作期間實作及利用分割區的方式，與針對已部署的模型實作及利用分割區的方式，可能大不相同。 請記住，在模型製作階段期間，您可能只會使用最後在已部署模型中之資料的子集。  
  
### <a name="processing-partitions"></a>處理分割區  
 針對已部署的模型，您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，或執行包含處理命令及指定處理選項和設定的指令碼，來進行處理。 使用 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]製作模型時，您可以從 [模型] 功能表或工具列使用 [處理] 命令，來執行處理作業。 您可以針對分割區、資料表或全部指定處理作業。  
  
 執行處理作業時，會使用資料連接建立資料來源的連接。 將新資料匯入至模型資料表中；為每個資料表重新建立關聯性和階層；以及重新計算導出資料行和量值中的計算。  
  
 透過進一步將資料表分成多個邏輯分割區，即可選擇性地決定每個分割區中所處理的資料，以及資料的處理時機和方式。 當您部署模型時，可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的 [分割區] 對話方塊手動完成分割區的處理，或使用指令碼執行處理命令。  
  
### <a name="partitions-in-the-model-workspace-database"></a>模型工作空間資料庫中的分割區  
 您可以使用 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]的 [分割區管理員] 建立新的分割區，以及編輯、合併或刪除分割區。 資料分割管理員會提供兩種模式，以選取資料表、 資料列和資料分割的資料行：資料表預覽模式和 SQL 查詢 模式。 所有分割區會使用 SQL 查詢定義；但是，透過資料表預覽模式，您可以預覽及選取要包含在分割區中的資料。 SQL 查詢會自動為您建立及驗證。 由於資料表預覽模式是 [編輯資料表屬性] 對話方塊中的相同資料表預覽，也是 [資料表匯入精靈] 之 [資料表預覽] 頁面中的相同資料表預覽，因此預覽中的最大資料列數為 50。  
  
### <a name="partitions-in-a-deployed-model-database"></a>已部署模型資料庫中的分割區  
 當您部署模型時，已部署模型資料庫的分割區會顯示為 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的資料庫物件。 您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的 [分割區] 對話方塊，為已部署的模型建立、編輯、合併及刪除分割區。 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中管理已部署模型的分割區超出本主題的範圍。 若要了解如何在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中管理資料分割，請參閱[建立及管理表格式模型資料分割 &#40;SSAS 表格式&#41;](create-and-manage-tabular-model-partitions-ssas-tabular.md)。  
  
##  <a name="bkmk_related_tasks"></a> 相關工作  
  
|主題|描述|  
|-----------|-----------------|  
|[在工作空間資料庫中建立及管理資料分割 &#40;SSAS 表格式&#41;](workspace-database-ssas-tabular.md)|描述如何使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]的分割區管理員，在模型工作空間資料庫中建立及管理分割區。|  
|[處理工作空間資料庫中的資料分割&#40;SSAS 表格式&#41;](process-partitions-in-the-workspace-database-ssas-tabular.md)|描述如何在模型工作空間資料庫中處理 (重新整理) 分割區。|  
  
## <a name="see-also"></a>另請參閱  
 [DirectQuery 模式 &#40;SSAS 表格式&#41;](directquery-mode-ssas-tabular.md)   
 [處理資料 &#40;SSAS 表格式&#41;](../process-data-ssas-tabular.md)  
  
  
