---
title: 資料分割 (Analysis Services-多維度資料) |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bf73453ce1bfec6d3cd55a73fe6e85938ee7b006
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="partitions-analysis-services---multidimensional-data"></a>資料分割 (Analysis Services - 多維度資料)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  資料分割是量值群組資料之一部分的容器。 無法從 MDX 查詢看到資料分割；所有的查詢都會反映量值群組的完整內容，不論針對此量值群組定義了多少個資料分割。 資料分割的資料內容是由資料分割的查詢繫結及分割運算式所定義。  
  
 簡單的 <xref:Microsoft.AnalysisServices.Partition> 物件是由基本資訊、分割定義、彙總設計等項目組成。 基本資訊包括資料分割的名稱、儲存模式、處理模式等等。 分割定義是指定 Tuple 或集合的 MDX 運算式。 分割定義與 StrToSet MDX 函數有相同的限制。 分割定義結合了 CONSTRAINED 參數，便可以在 Cube 中使用維度、階層、層級和成員名稱、索引鍵、唯一名稱或其他具名物件，但是不能使用 MDX 函數。 彙總設計是可在多個資料分割之間共用之彙總定義的集合。 預設值是取自父 Cube 的彙總設計。  
  
 資料分割由[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]來管理及儲存 cube 中的資料和彙總為量值群組。 每一個量值群組至少都有一個資料分割；當定義該量值群組時，就會建立此資料分割。 為量值群組建立新的資料分割時，新的資料分割會加入到該量值群組已存在的資料分割集合中。 量值群組會反映其所有資料分割中所包含的結合資料。 這表示，您必須確定量值群組中某個資料分割的資料不包含該量值群組中其他任何資料分割的資料，以確保資料不會在量值群組中反映一次以上。 量值群組的原始資料分割以 Cube 之資料來源檢視中的單一事實資料表為依據。 一個量值群組有多個資料分割時，每個資料分割都可以在資料來源檢視或 Cube 之基礎關聯式資料來源中參考不同的資料表。 如果將每個資料分割限制到資料表中的不同資料列，則量值群組中的多個資料分割即可參考相同的資料表。  
  
 資料分割是管理 Cube 強大而有彈性的方式，特別是對大型的 Cube。 例如，內含銷售資訊的 Cube 可以包含過去每年資料的資料分割，以及今年每一季的資料分割。 將目前的資訊加入到 Cube 時，只需要處理目前這一季的資料分割；處理較少量的資料將會縮短處理時間而提升處理效能。 在一年的結尾，四季的資料分割可以合併到這一年的單一資料分割以及新年度第一季所建立的新資料分割當中。 此外，可以在資料倉儲載入及 Cube 處理程序當中自動化這個新資料分割的建立程序。  
  
 Cube 的商務使用者看不到資料分割。 不過，管理員可以設定、加入或卸除資料分割。 每個資料分割儲存在個別的檔案集內。 每個資料分割的彙總資料都可以儲存在定義資料分割的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上、另一個 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上，或用於提供資料分割之來源資料的資料來源中。 資料分割允許 Cube 的來源資料和彙總資料，散發在多個硬碟上與多部伺服器電腦間。 針對中型到大型的 Cube，資料分割可以大幅提升查詢效能、載入效能和簡化 Cube 的維護。  
  
 每個資料分割的儲存模式，可以不受量值群組中其他資料分割的影響，單獨設定。 您可以使用於源資料位置、儲存模式、主動式快取和彙總設計之選項的任意組合來儲存資料分割； 即時 OLAP 和主動式快取的選項可讓您在設計資料分割時，平衡查詢速度與延遲。 儲存選項也可以套用到相關的維度，以及量值群組中的事實。 這種彈性可讓您依據您的需求來設計適當的 Cube 儲存策略。 如需詳細資訊，請參閱[磁碟分割儲存模式及處理](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-partition-storage-modes-and-processing.md)，[彙總和彙總設計](../../analysis-services/multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)和[主動式快取&#40;分割&#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md).  
  
## <a name="partition-structure"></a>資料分割結構  
 資料分割的結構必須符合其量值群組的結構，這也就表示，定義此量值群組的量值也必須定義於此資料分割中，連同所有相關的維度。 因此，建立資料分割時，它會自動繼承為該量值群組所定義的相同量值集合和相關維度。  
  
 但是量值群組中的每一個資料分割都可以有不同的事實資料表，而這些事實資料表可以來自不同的資料來源。 當量值群組中的不同資料分割有不同的事實資料表時，這些資料表必須非常類似，才能維護此量值群組的結構；這也就表示，處理查詢對於所有資料分割的所有事實資料表都會傳回相同的資料行和相同的資料類型。  
  
 當不同資料分割的事實資料表是來自不同的資料來源時，任何相關維度的來源資料表和任何中繼事實資料表，也都必須存在於所有資料來源中，而且在所有資料庫中的結構都必須相同。 此外，用於定義與量值群組相關之 Cube 維度屬性的所有維度資料表資料行，都必須存在於所有的資料來源中。 如果資料分割來源資料表與量值群組之來源資料表的結構完全相同，則不需要在資料分割的來源資料表與相關維度資料表之間定義所有的聯結。  
  
 某些事實資料表中會有不是用於定義量值群組之量值的資料行，而某些事實資料表中則不會有這樣的資料行。 同樣地，某些資料庫中會有不是用於定義相關維度資料表之屬性的資料行，而某些資料庫中則不會有這樣的資料行。 某些資料庫中會有不是用於事實資料表和相關維度資料表的資料表，而某些資料庫中則不會有這樣的資料表。  
  
## <a name="data-sources-and-partition-storage"></a>資料來源與資料分割儲存  
 資料分割的基礎是資料來源中的資料表或檢視，或資料來源檢視中的資料表或具名查詢。 資料分割資料的儲存位置是由資料來源繫結所定義。 通常，您可以水平或垂直地分割量值群組：  
  
-   在水平分割的量值群組中，量值群組的每個資料分割是以個別的資料表為依據。 這類型的資料分割適用於將資料分隔到多份資料表時。 例如，部份關聯式資料庫針對每個月的資料會有個別的資料表。  
  
-   在垂直分割的量值群組中，量值群組是以單一資料表為基礎，而每一個資料分割都是根據篩選資料分割之資料的來源系統查詢。 例如，若單一資料表包含數個月份的資料，仍可以套用 Transact-SQL WHERE 子句來對每一個資料分割傳回個別月份資料，根據月份分割量值群組。  
  
 每一個資料分割都會有儲存設定，用以決定是要將該資料分割的資料和彙總儲存在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的本機執行個體中，還是儲存在使用另一個 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的遠端資料分割中； 這些儲存設定也可以指定儲存模式，以及指定是否使用主動式快取來控制資料分割的延遲。 如需詳細資訊，請參閱[磁碟分割儲存模式及處理](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-partition-storage-modes-and-processing.md)，[主動式快取&#40;分割&#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)，和[遠端資料分割](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-remote-partitions.md)。  
  
## <a name="incremental-updates"></a>累加式更新  
 當您在多資料分割量值群組中建立和管理資料分割時，必須採取特別注意事項以確保 Cube 資料正確。 雖然這些注意事項通常都不會套用到單一資料分割量值群組，但是當您以累加方式更新資料分割時則會予以套用。 當您以累加方式更新資料分割時，會建立新的暫存資料分割，而這個資料分割的結構與來源資料分割的結構相同。 這時會處理暫存資料分割，再與來源資料分割合併。 因此，您必須確定擴展暫存資料分割的處理查詢不會複製已經存在於現有資料分割中的任何資料。  
  
## <a name="see-also"></a>另請參閱  
 [設定量值屬性](../../analysis-services/multidimensional-models/configure-measure-properties.md)   
 [多維度模型中的 cube](../../analysis-services/multidimensional-models/cubes-in-multidimensional-models.md)  
  
  
