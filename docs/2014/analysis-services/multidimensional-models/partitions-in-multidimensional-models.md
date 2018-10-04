---
title: 多維度模型中的資料分割 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 26e01dc7-fa49-4b1f-99eb-7799d1b4dcd2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8caec3620a5f7c0df1e3a5d0558272b1a2fb7bfa
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48164188"
---
# <a name="partitions-in-multidimensional-models"></a>多維度模型中的分割區
  在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中， *「分割區」* (Partition) 提供載入量值群組之事實資料的實體儲存體。 系統會自動為每個量值群組建立一個分割區，但通常會建立其他分割區以進一步分割資料，因此處理效能更佳且查詢效能更快。  
  
 因為可以在一部或多部伺服器上獨立及平行處理分割區，因此處理進行得更有效率。 因為可設定每個分割區使用儲存模式和彙總最佳化，藉此縮短回應時間，因此查詢執行速度更快。 例如，針對包含較新資料的分割區選擇 MOLAP 儲存，通常會比 ROLAP 更快。 同樣地，如果您依日期分割，包含較新資料的分割區，這會比包含較舊資料 (較少存取) 的分割區，具有更高的最佳化。 請注意，改變分割區使用的儲存和彙總設計，會對未來的合併作業造成負面影響。 因此最佳化個別分割區之前，請務必考慮合併是否為分割區管理策略中不可或缺的一部分。  
  
> [!NOTE]  
>  支援在 Business Intelligence 版與 Enterprise 版中使用多個分割區。 Standard 版不支援多個分割區。 如需詳細資訊，請參閱＜ [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)＞。  
  
## <a name="important-considerations-when-designing-a-partitioning-strategy"></a>設計分割區策略時的重要考量  
 Cube 資料的完整性是仰賴 Cube 分割區之間散發的資料，以讓分割區間沒有重複的資料。 若資料是從分割區來彙總，則任何多個分割區中出現的資料元素都會被視為不同資料元素而彙總。 這會導致不正確的彙總，以及提供使用者錯誤的資料。 例如，若產品 X 的銷售交易在兩個分割區的事實資料表中發生重複，則產品 X 銷售的彙總會包括重複交易的兩次計算。  
  
 您可以利用整體儲存和資料更新策略中的合併分割區功能。 只有在分割區具有相同儲存模式及彙總設計時，才可以進行合併。 若要建立適合日後進行合併的分割區，您可以在建立分割區時，複製其他分割區的彙總設計。 您也可以在建立分割區後進行編輯，以複製其他分割區的彙總設計。 您必須小心執行分割區合併，以避免產生的分割區中，出現重複的資料，而導致 Cube 資料不精確。  
  
## <a name="local-partitions"></a>本機分割區  
 本機分割區是在一個伺服器上定義、處理以及儲存的分割區。 如果您在 Cube 中有很多量值群組，您可能需要進行分割區，讓處理在所有分割區上平行執行。 優點是平行處理會提供更快的執行速度。 因為分割區處理作業並不要求先後完成順序，可以平行執行。 如需詳細資訊，請參閱[建立及管理本機資料分割 &#40;Analysis Services&#41;](create-and-manage-a-local-partition-analysis-services.md)。  
  
## <a name="remote-partitions"></a>遠端資料分割  
 遠端分割區是在一個伺服器上定義的分割區，但在另一個伺服器上處理和儲存。 如果您要將資料和中繼資料的儲存體散發至多個伺服器，請使用遠端分割區。 通常，當您從開發環境轉換到實際環境時，分析的資料大小會成長數倍以上。 對付如此大量的資料區塊，一種可能的替代方法是將資料散發在多部電腦上。 這不僅是因為一部電腦無法存放所有資料，更是因為您希望有多部電腦可以平行處理資料。 如需詳細資訊，請參閱 <<c0> [ 建立及管理遠端資料分割&#40;Analysis Services&#41;](create-and-manage-a-remote-partition-analysis-services.md)。</c0>  
  
## <a name="aggregations"></a>Aggregations  
 彙總是 Cube 資料的預先計算摘要，可幫助啟用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 以提供快速查詢回應。 您可以透過設定儲存限制、改善效能，或在彙總建立程序執行一段時間後隨時停止，以控制為量值群組建立的彙總數目。 彙總愈多不一定愈好。 每個新彙總都會佔用磁碟空間並增加處理時間。 建議建立彙總以改善 30% 的效能，然後僅在測試或經驗需要時，才增加數目。如需詳細資訊，請參閱[設計彙總 &#40;Analysis Services - 多維度&#41;](designing-aggregations-analysis-services-multidimensional.md)。  
  
## <a name="partition-merging-and-editing"></a>分割區合併和編輯  
 如果兩個分割區使用相同的彙總設計，您就可以將兩者合併為一個分割區。 例如，假設您有一個依照月份分割的存貨維度，則在每一個月底，您可以合併該月分割區和現有的年初至今的分割區。 如此，可以快速處理和分析當月分割區，而當年剩餘的月份只需要在合併時重新處理即可。 重新處理需要較長的處理時間，所以不需要經常執行。 如需管理分割區合併處理序的詳細資訊，請參閱[在 Analysis Services 中合併分割區&#40;SSAS-多維度&#41;](merge-partitions-in-analysis-services-ssas-multidimensional.md)。 若要使用來編輯 cube 分割區**資料分割**索引標籤，Cube 設計師中，請參閱[編輯或刪除的資料分割&#40;Analysis Services-多維度&#41;](edit-or-delete-partitions-analyisis-services-multidimensional.md)。  
  
## <a name="related-topics"></a>相關主題  
  
|主題|描述|  
|-----------|-----------------|  
|[建立及管理本機資料分割&#40;Analysis Services&#41;](create-and-manage-a-local-partition-analysis-services.md)|包含如何使用篩選或不含重複資料的不同事實資料表，來分割資料的詳細資訊。|  
|[設定分割區儲存&#40;Analysis Services-多維度&#41;](set-partition-storage-analysis-services-multidimensional.md)|描述如何設定分割區的儲存。|  
|[編輯或刪除分割區&#40;Analysis Services-多維度&#41;](edit-or-delete-partitions-analyisis-services-multidimensional.md)|描述如何檢視和編輯分割區。|  
|[Analysis Services 中合併資料分割&#40;SSAS-多維度&#41;](merge-partitions-in-analysis-services-ssas-multidimensional.md)|包含如何合併含有不同事實資料表或不同資料配量的分割區，而不會產生重複資料。|  
|[設定分割區回寫](set-partition-writeback.md)|提供啟用分割區寫入功能的指示。|  
|[建立和管理遠端資料分割&#40;Analysis Services&#41;](create-and-manage-a-remote-partition-analysis-services.md)|描述如何建立及管理遠端分割區。|  
  
  
