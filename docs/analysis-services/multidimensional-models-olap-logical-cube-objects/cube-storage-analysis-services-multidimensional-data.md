---
title: Cube 儲存體 (Analysis Services-多維度資料) |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0f1b06558b356e4542a60ffc13a317b5c9fcbd25
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="cube-storage-analysis-services---multidimensional-data"></a>Cube 儲存體 (Analysis Services - 多維度資料)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  儲存體可以只包含 Cube 中繼資料，或是包含事實資料表的所有來源資料，以及與量值群組相關之維度所定義的彙總。 儲存的資料量取決於選取的儲存模式和彙總數目。 直接儲存的資料數量會影響查詢效能； [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 使用數個技術儲存 cube 資料和彙總所需的空間最小化：  
  
-   儲存選項可讓您選取最適合 Cube 資料的儲存模式和位置。  
  
-   使用複雜的演算法設計有效的摘要彙總，以減少儲存體的需求並且不犧牲速度。  
  
-   儲存體不會配置給空資料格。  
  
 儲存是依照每一個資料分割來定義，Cube 中的每一個量值群組至少有一個資料分割。 如需詳細資訊，請參閱[分割&#40;Analysis Services-多維度資料&#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)，[磁碟分割儲存模式及處理](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-partition-storage-modes-and-processing.md)，[量值和量值群組](../../analysis-services/multidimensional-models/measures-and-measure-groups.md)，和[多維度模型中建立量值和量值群組](../../analysis-services/multidimensional-models/create-measures-and-measure-groups-in-multidimensional-models.md)。  
  
## <a name="partition-storage"></a>資料分割儲存  
 量值群組的儲存體分成多個資料分割。 資料分割可讓您將量值群組散發至單一伺服器或跨多部伺服器的不連續區段，以及最佳化儲存和查詢效能。 量值群組中的每一個資料分割可以不同資料來源作為基礎，並使用不同儲存設定來儲存。  
  
 您可以在建立資料分割時指定它的資料來源。 您也可以變更任何現有資料分割的資料來源。 量值群組可以垂直或水平分割。 垂直分割之量值群組中的每一個資料分割，是以單一來源資料表的篩選檢視作為基礎。 例如，如果量值群組是以包含數年資料的單一資料表為基礎，則您可以為每年的資料建立個別的資料分割。 反之，水平分割之量值群組中的每個資料分割都是以個別資料表為基礎。 如果資料來源是將每年的資料儲存在個別資料表中，則您可以使用水平資料分割。  
  
 量值群組一開始建立時，是使用它們建立時所在之量值群組的相同儲存設定。 儲存設定決定詳細資料和彙總資料是要以多維度格式儲存在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上、以關聯格式儲存在來源伺服器上，或是這兩種方式的結合。 儲存設定也決定是否使用主動式快取來自動處理 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 上所儲存之多維度資料的來源資料變更。  
  
 使用者看不到 Cube 的資料分割。 然而，不同資料分割之儲存設定的選擇會影響資料的立即性、使用的磁碟空間量，以及查詢效能。 資料分割可儲存於多個 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體中。 這提供 Cube 儲存體的叢集方式，並跨 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器散發工作負載。 如需詳細資訊，請參閱[磁碟分割儲存模式及處理](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-partition-storage-modes-and-processing.md)，[遠端資料分割](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-remote-partitions.md)，和[分割&#40;Analysis Services-多維度資料&#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md).  
  
## <a name="linked-measure-groups"></a>連結量值群組  
 這需要大量磁碟空間來儲存不同 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上之 Cube 的多個副本，但您可將量值群組的副本取代為連結量值群組，以大幅減少所需的空間。 連結量值群組的基礎是位於相同或不同 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上之另一個 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫中之 Cube 的量值群組。 連結量值群組也可以與來自相同來源 Cube 的連結維度一起使用。 連結維度和量值群組使用來源 Cube 的彙總，而沒有自己的資料儲存需求。 因此，透過維護某個資料庫中的來源量值群組和維度，以及在其他資料庫的 Cube 中建立連結 Cube 和維度，您即可以節省用於進行儲存的磁碟空間。 如需詳細資訊，請參閱[Linked Measure Groups](../../analysis-services/multidimensional-models/linked-measure-groups.md)。  
  
## <a name="see-also"></a>另請參閱  
 [彙總和彙總設計](../../analysis-services/multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)  
  
  
