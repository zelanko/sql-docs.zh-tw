---
title: 處理需求和考量 （資料採礦） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], objects
- mining structures [Analysis Services], processing
- mining models [Analysis Services], processing
ms.assetid: f7331261-6f1c-4986-b2c7-740f4b92ca44
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 181e2a367f6196d50f90aee77ca9590f55ba0ce4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62733060"
---
# <a name="processing-requirements-and-considerations-data-mining"></a>處理需求和考量 (資料採礦)
  此主題描述在處理資料採礦物件時要記住的一些技術考量。 如需什麼是處理以及如何將處理套用至資料採礦的一般說明，請參閱 [處理資料採礦物件](processing-data-mining-objects.md)。  
  
 [查詢關聯式存放區](#bkmk_QueryReqs)  
  
 [處理採礦結構](#bkmk_ProcessStructures)  
  
 [處理採礦模型](#bkmk_ProcessModels)  
  
##  <a name="bkmk_QueryReqs"></a> 在處理期間查詢關聯式存放區  
 對於資料採礦，處理可分成三個階段：查詢來源資料、判斷原始統計資料，以及使用模型定義和演算法來定型採礦模型。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器會發出查詢給提供原始資料的資料庫。 這個資料庫可能是 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或舊版 SQL Server 資料庫引擎的執行個體。 當您處理資料採礦結構時，來源中的資料會傳送到採礦結構，並以新的壓縮格式保存在磁碟上。 系統並不會處理資料來源中的每個資料行，而只會處理包含在採礦結構中的資料行 (由繫結來定義)。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會使用這項資料來建置所有資料和離散化資料行的索引，而且會建立連續資料行的個別索引。 系統會針對每個巢狀資料表發出一個查詢，以便建立索引，而且會針對每個巢狀資料表產生額外的查詢，以便處理每對巢狀資料表與案例資料表之間的關聯性。 建立多個查詢的原因是要處理特殊的內部多維度資料存放區。 您可以透過設定伺服器屬性 `DatabaseConnectionPoolMax`，限制 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 傳送至關聯式存放區的查詢數目。 如需詳細資訊，請參閱 [OLAP 屬性](../server-properties/olap-properties.md)。  
  
 當您處理模型時，模型並不會從資料來源重新讀取資料，而是從採礦結構取得資料摘要。 使用所建立的 Cube，連同快取索引及快取的案例資料之後，伺服器就會建立獨立的執行緒來定型模型。  
  
 如需版本的詳細資訊[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，支援平行模型處理，請參閱 <<c2> [ 支援的 SQL Server 2012 的版本功能](https://go.microsoft.com/fwlink/?linkid=232473)(https://go.microsoft.com/fwlink/?linkid=232473)。  
  
##  <a name="bkmk_ProcessStructures"></a> 處理採礦結構  
 採礦結構可以與所有相依模型一起處理，也可以單獨處理。 在預期某些模型需要長時間來處理並且您想要延遲該作業時，分開處理採礦結構與模型可能會很有用。  
  
 如需詳細資訊，請參閱 [處理採礦結構](process-a-mining-structure.md)。  
  
 如果您希望節省硬碟空間，請注意 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會在本機保留採礦結構快取。 亦即，它會將所有培訓資料寫出至本機硬碟。 如果不要快取資料，您可以設定採礦結構的 <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> 屬性，將預設值變更為 `ClearAfterProcessing`。 這會在處理模型之後終結快取，但是，它也會在採礦結構上停用鑽研。 如需詳細資訊，請參閱 [鑽研查詢 &#40;資料採礦&#41;](drillthrough-queries-data-mining.md)。  
  
 同時，如果您清除快取，將無法使用鑑效組測試集；如果已經定義一個鑑效組測試集，將會遺失該測試集資料分割的定義。 如需鑑效組測試集的詳細資訊，請參閱 [定型和測試資料集](training-and-testing-data-sets.md)。  
  
##  <a name="bkmk_ProcessModels"></a> 處理採礦模型  
 您可以分開處理採礦模型與其相關聯的採礦結構，或是將以結構為基礎的所有模型與此結構一起處理。  
  
 如需詳細資訊，請參閱 [處理採礦模型](process-a-mining-model.md)。  
  
 但在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，您無法複選多個要與結構一起處理的採礦模型。 如果您需要控制所處理的模型，則必須個別選取這些模型，或使用 XMLA 或 DMX 循序處理多個模型。  
  
## <a name="when-reprocessing-is-required"></a>何時需要重新處理  
 您定義的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 模型必須經過處理之後才能開始使用。 每當變更採礦模型結構、更新定型資料、變更現有的採礦模型或將新的採礦模型加入結構中時，您也必須重新處理採礦模型。  
  
 在以下案例中也會處理採礦模型：  
  
 **部署專案**:根據專案設定和專案的目前狀態，在專案中會處理採礦模型通常是完整部署專案時。  
  
 除非 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器上已有先前處理的版本，且尚無任何結構性變更，否則，起始部署時會自動開始處理。 您可以從下拉式清單中選取 [部署方案]，或按 F5 鍵來部署專案。 您可以  
  
 如需如何設定 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署屬性來控制採礦模型部署方式的詳細資訊，請參閱 [部署資料採礦方案](deployment-of-data-mining-solutions.md)。  
  
 **移動採礦模型**:當您使用 EXPORT 命令移動採礦模型時，會匯出模型的定義，其中包含所要提供資料給模型的採礦結構的名稱。  
  
 針對以下案例使用 EXPORT 和 IMPORT 命令進行重新處理的需求：  
  
-   採礦結構存在於目標執行個體上，並且採礦結構處於未處理狀態。  
  
     結構和模型都必須重新處理。  
  
-   採礦結構存在於目標執行個體上，並且採礦結構已經處理。 只匯出了採礦模型。  
  
     模型不需處理即可使用。  
  
-   也透過使用 WITH DEENDENCIES 關鍵字匯出了採礦結構定義。  
  
     結構和模型都必須重新處理。  
  
 如需詳細資訊，請參閱 [匯出和匯入資料採礦物件](export-and-import-data-mining-objects.md)。  
  
## <a name="see-also"></a>另請參閱  
 [採礦結構 &#40;Analysis Services - 資料採礦&#41;](mining-structures-analysis-services-data-mining.md)   
 [採礦結構 &#40;Analysis Services - 資料採礦&#41;](mining-structures-analysis-services-data-mining.md)   
 [多維度模型物件處理](../multidimensional-models/processing-a-multidimensional-model-analysis-services.md)  
  
  
