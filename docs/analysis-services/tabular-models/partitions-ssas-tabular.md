---
title: 分割區 |Microsoft 文件
ms.custom: ''
ms.date: 04/10/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 708b9bdf-8c0b-4476-809a-8f616be23a58
caps.latest.revision: 20
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: b012ae919b376151a465557941739df847310b1e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="partitions"></a>資料分割
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  分割區會將一個資料表分割成多個邏輯部分。 接著，每個分割區可以不受其他分割區的影響，單獨處理 (重新整理)。 在模型製作期間使用分割區 對話方塊，在 SSDT 中的建立分割區套用至模型工作空間資料庫。 部署模型之後，為模型工作空間資料庫定義的分割區，會複製到已部署的模型資料庫中。 此外，您可以建立，使用分割區 對話方塊，在 SSMS 中的管理已部署的模型資料庫的資料分割。  本主題提供資訊說明使用 [資料分割管理員] 對話方塊在 SSDT 中的模型撰寫期間建立的資料分割。 如需建立和管理已部署模型的分割區資訊，請參閱[建立及管理表格式模型資料分割](../../analysis-services/tabular-models/create-and-manage-tabular-model-partitions-ssas-tabular.md)。  
  
##  <a name="bkmk_benefits"></a> 優點  
 表格式模型中的分割區，會將一個資料表分割成多個邏輯分割區物件。 接著，每個資料分割可以不受其他資料分割的影響，單獨進行處理。 例如，資料表的其中一些資料列集可能包含不常變更的資料，而其他一些資料列集則包含經常變更的資料。 在此情況下，如果您只想處理部分資料，則不需要處理所有資料。 分割區可讓您將需要經常處理的資料部分，與不常處理的資料加以分割。  
  
 有效的模型設計能善加利用分割區，以避免不必要的處理及 Analysis Services 伺服器上之後續處理器的負載，同時，還可確保資料的處理和重新整理頻率能反映資料來源的最新資料。 您在模型製作期間實作及利用分割區的方式，與針對已部署的模型實作及利用分割區的方式，可能大不相同。 請記住，在模型製作階段期間，您可能只會使用最後在已部署模型中之資料的子集。  
  
### <a name="processing-partitions"></a>處理分割區  
 對於已部署的模型，請使用 SSMS，或藉由執行包含處理命令及指定處理選項和設定的指令碼進行處理。 當使用 SSDT 製作模型時，您可以使用處理命令，從 [模型] 功能表或工具列來執行處理作業。 您可以針對分割區、資料表或全部指定處理作業。  
  
 執行處理作業時，會使用資料連接建立資料來源的連接。 將新資料匯入至模型資料表中；為每個資料表重新建立關聯性和階層；以及重新計算導出資料行和量值中的計算。  
  
 透過進一步將資料表分成多個邏輯分割區，即可選擇性地決定每個分割區中所處理的資料，以及資料的處理時機和方式。 當您部署模型時，可以使用分割區 對話方塊，在 SSMS 中，手動完成分割區的處理，或使用指令碼執行處理命令。  
  
### <a name="partitions-in-the-model-workspace-database"></a>模型工作空間資料庫中的分割區  
 您可以建立新的資料分割、 編輯、 合併或刪除使用資料分割管理員在 SSDT 中的資料分割。 根據您撰寫之模型的相容性層級，資料分割管理員會提供兩種模式來選取資料表、 資料列和資料分割的資料行： 表格式 1400年模型，使用 M 查詢、 定義資料分割，或者您可以使用設計模式中開啟查詢編輯器。 對於表格式 1100、 1103、 1200年模型中，使用資料表預覽模式和 SQL 查詢模式。 
  
### <a name="partitions-in-a-deployed-model-database"></a>已部署模型資料庫中的分割區  
 當您部署模型時，已部署的模型資料庫的分割區會以在 SSMS 中的資料庫物件。 您可以建立、 編輯、 合併，並使用分割區 對話方塊，在 SSMS 中的刪除已部署模型的分割區。 管理已部署的模型，在 SSMS 中的分割區超出本主題的範圍。 若要了解如何管理在 SSMS 中的資料分割，請參閱[建立及管理表格式模型資料分割](../../analysis-services/tabular-models/create-and-manage-tabular-model-partitions-ssas-tabular.md)。  
  
##  <a name="bkmk_related_tasks"></a> Related tasks  
  
|主題|Description|  
|-----------|-----------------|  
|[在工作空間資料庫中建立及管理資料分割](../../analysis-services/tabular-models/create-and-manage-partitions-in-the-workspace-database-ssas-tabular.md)|描述如何建立及管理模型工作空間資料庫中的資料分割在 SSDT 中使用資料分割管理員。|  
|[在工作空間資料庫中處理資料分割](../../analysis-services/tabular-models/process-partitions-in-the-workspace-databse-ssas-tabular.md)|描述如何在模型工作空間資料庫中處理 (重新整理) 分割區。|  
  
## <a name="see-also"></a>另請參閱  
 [DirectQuery 模式](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)   
 [處理資料](../../analysis-services/tabular-models/process-data-ssas-tabular.md)  
  
  
