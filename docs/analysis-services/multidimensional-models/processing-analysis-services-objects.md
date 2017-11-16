---
title: "處理 Analysis Services 物件 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- OLAP objects [Analysis Services], processing
- OLAP objects [Analysis Services]
ms.assetid: c7e1f66f-16ca-43da-b8c7-4d3e1fa8b58d
caps.latest.revision: 44
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 58e0a8da7c8bfeae9d661dc78d264218c7c19b81
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="processing-analysis-services-objects"></a>處理 Analysis Services 物件
  處理會影響下列 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件類型： [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫、Cube、維度、量值群組、資料分割，以及資料採礦結構和模型。 您可以針對每一個物件，指定物件的處理層級，或者指定 [處理預設] 選項，讓 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 自動選取最佳的處理層級。 如需處理每一個物件之不同層級的詳細資訊，請參閱[處理選項和設定 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md)。  
  
 您必須了解處理行為的後果，以減少任何不良影響。 例如，完整處理維度會自動將相依於該維度的所有資料分割設定為尚未處理狀態。 如此會造成受影響的 Cube 無法供查詢使用，直到相依的資料分割進行處理為止。  
  
 本主題包含下列各節：  
  
 [處理資料庫](#bkmk_procdb)  
  
 [處理維度](#bkmk_procdim)  
  
 [處理 Cube](#bkmk_proccube)  
  
 [處理量值群組](#bkmk_procmeasure)  
  
 [處理資料分割](#bkmk_procpartition)  
  
 [處理資料採礦結構和模型](#bkmk_procdm)  
  
##  <a name="bkmk_procdb"></a> 處理資料庫  
 在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，資料庫包含物件但不包含資料。 當您處理資料庫時，會指示伺服器遞迴處理將資料儲存在模型中的物件，例如維度、資料分割、採礦結構和採礦模型。  
  
 處理資料庫時，都會處理資料庫包含的部分或所有資料分割、維度以及採礦模型。 實際處理類型會依每個物件的狀態以及您選取的處理選項而有所不同。 如需詳細資訊，請參閱[處理選項和設定 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md)。  
  
##  <a name="bkmk_proccube"></a> 處理 Cube  
 Cube 可視為量值群組和資料分割的包裝函數物件。 Cube 是由維度，以及一個或多個儲存在資料分割中的量值所組成。 維度會定義資料在 Cube 如何配置。 當您處理 Cube 時，會發出 SQL 查詢來擷取事實資料表中的值，以適當的量值來擴展 Cube 中的每一個成員。 針對 Cube 中之節點的任何特定路徑，都有一個值或可計算的值。  
  
 處理 Cube 時， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會處理 Cube 中尚未處理的任何維度，以及 Cube 中量值群組內的部分或所有資料分割。 實際處理結果會視物件在開始處理時的狀態，以及您選取的處理選項而定。 如需處理選項的詳細資訊，請參閱[處理選項和設定 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md)。  
  
 處理 Cube 會建立電腦可讀取的檔案，這些檔案儲存相關事實資料。 如果建立了彙總，則會儲存在彙總資料檔案中。 接著，可以從 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 的物件總管或下列項目中的方案總管中瀏覽 Cube： [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]  
  
##  <a name="bkmk_procdim"></a> 處理維度  
 處理維度時， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會編寫查詢並對維度資料表執行查詢，以傳回處理時所需的資訊。  
  
|Country|銷售區域|State|  
|-------------|------------------|-----------|  
|United States|West|California|  
|United States|West|Oregon|  
|United States|West|Washington|  
  
 處理本身會將表格式資料轉換成可用的階層。 這些階層是完全相互連貫的成員名稱，在內部是由唯一數字路徑來表示。 下面的範例是階層的文字表示法。  
  
||  
|-|  
|[United States]|  
|[United States].[West]|  
|[United States].[West].[California]|  
|[United States].[West].[Oregon]|  
|[United States].[West].[Washington]|  
  
 維度處理不會建立或更新導出成員，這些都是在 Cube 層級定義的。 導出成員會在更新 Cube 定義時受到影響。 此外，維度處理也不會建立或更新彙總。 然而，維度處理可能會造成彙總遭到卸除。 只有在資料分割處理期間才會建立或更新彙總。  
  
 處理維度時，請注意此維度可能在數個 Cube 中使用。 處理維度時，這些 Cube 是標示為尚未處理，而且無法供查詢使用。 若要同時處理維度和相關的 Cube，請使用批次處理設定。 如需詳細資訊，請參閱 [批次處理 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/batch-processing-analysis-services.md)。  
  
##  <a name="bkmk_procmeasure"></a> 處理量值群組  
 處理量值群組時， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會處理量值群組內的部分或所有資料分割，以及參與量值群組的任何尚未處理的維度。 處理作業的實際結果會視您選取的處理選項而定。 您可以在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中處理一個或多個量值群組，不影響 Cube 中的其他量值群組。  
  
> [!NOTE]  
>  您可以用程式設計方式或使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]來處理個別的量值群組。 您無法在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中處理個別的量值群組，不過，您可以透過資料分割來處理。  
  
##  <a name="bkmk_procpartition"></a> 處理資料分割  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的有效管理包括資料的分割。 資料分割處理是唯一的，因為它要考量硬碟的使用和空間條件約束，還有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]所加諸的資料結構限制。 若要使查詢回應時間快速及處理輸送量提高，您必須定期建立、處理和合併資料分割。 在資料分割合併期間，辨識及管理整合重複資料的機會非常重要。 如需詳細資訊，請參閱[在 Analysis Services 中合併分割區 &#40;SSAS - 多維度&#41;](../../analysis-services/multidimensional-models/merge-partitions-in-analysis-services-ssas-multidimensional.md)。  
  
 在處理資料分割時，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會處理資料分割及資料分割中存在的任何尚未處理的維度，視您選取的處理選項而定。 在處理方面，使用資料分割有多項優點。 您可以在不影響 Cube 中的其他資料分割的情況下，處理一個資料分割。 在儲存受資料格回寫限制的資料時，資料分割很有用。 回寫功能可讓使用者透過將新資料寫回資料分割中查看所預期的變更效果，以執行假設分析。 如果您使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的資料格回寫功能，則需要回寫資料分割。 平行處理分割區很有用，因為 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 可以更有效率地運用處理能力，且可以明顯降低總處理時間。 您也可以循序處理分割區。  
  
##  <a name="bkmk_procdm"></a> 處理資料採礦結構和模型  
 採礦結構會定義用於建立資料採礦模型的資料網域。 一個採礦結構可以包含一個以上的採礦模型。 您可以分開處理採礦結構及其相關聯的採礦模型。 當您分開處理採礦結構時，會以資料來源中的定型資料來擴展它。  
  
 處理資料採礦模型時，定型資料會透過採礦模型演算法來傳遞，使用資料採礦演算法定型模型，並建立內容。 如需資料採礦模型物件的詳細資訊，請參閱[採礦結構 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)。  
  
 如需處理採礦結構和模型的詳細資訊，請參閱[處理需求和考量 &#40;資料採礦&#41;](../../analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)。  
  
## <a name="see-also"></a>另請參閱  
 [處理的工具和方式 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/tools-and-approaches-for-processing-analysis-services.md)   
 [批次處理 &#40;Analysis Services &#41;](../../analysis-services/multidimensional-models/batch-processing-analysis-services.md)   
 [處理多維度模型 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)  
  
  

