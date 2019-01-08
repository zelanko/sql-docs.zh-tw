---
title: 彙總及彙總設計 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- aggregations [Analysis Services], about aggregations
- storage [Analysis Services], aggregations
- Storage Design Wizard
- data summary [Analysis Services]
- data storage [Analysis Services]
- storing data [Analysis Services], aggregations
- aggregations [Analysis Services]
ms.assetid: 35bd8589-39fa-4e0b-b28f-5a07d70da0a2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4d522f0da9bbaad8233bf0e1d1d3f18d6db56c4d
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52529186"
---
# <a name="aggregations-and-aggregation-designs"></a>彙總和彙總設計
  <xref:Microsoft.AnalysisServices.AggregationDesign> 物件會定義可在多個資料分割之間共用的一組彙總定義。  
  
 <xref:Microsoft.AnalysisServices.Aggregation> 物件表示在維度的某個資料粒度上之量值群組資料的摘要。  
  
 簡單的 <xref:Microsoft.AnalysisServices.Aggregation> 物件是由基本資訊和維度所組成。 基本資訊包括彙總的名稱、識別碼、註解和描述。 維度是包含此維度之資料粒度屬性清單的 <xref:Microsoft.AnalysisServices.AggregationDimension> 物件集合。  
  
 彙總是預先計算之分葉資料格的資料摘要， 彙總會藉由在詢問問題之前準備答案來縮短查詢回應時間。 例如，當資料倉儲事實資料表包含數十萬個資料列時，如果在查詢階段必須掃描和加總事實資料表的所有資料列才能計算出答案，則要求特定產品線每週總銷售量的查詢會需要花很多時間才會有答案。 但若已經預先計算好回答這個查詢的摘要資料，則幾乎可以立即回應。 在處理期間預先計算摘要資料，是 OLAP 技術之快速回應時間的基礎。  
  
 Cube 是 OLAP 技術將摘要資料組織成多維度結構的方式。 維度及其屬性階層會反映可要求得到 Cube 的查詢。 彙總儲存在資料格的多維度結構中，由維度指定其座標。 例如，「1998 年西北地區 X 產品的銷售如何？」這個問題 包含三個維度 (Product、Time 和 Geography) 和一個量值 (Sales)。 在 Cube 內之指定座標 (product X, 1998, Northwest) 上的資料格值就是答案，其為單一數值。  
  
 其他問題可能會傳回多個值。 例如，「1998 年分區分季的硬體產品銷售量為何？ 」，這樣的查詢會從滿足所指定條件的座標位置傳回儲存格組。 查詢所傳回的資料格數目會根據產品維度之硬體層級的項目數目、1998 年四季，以及地理位置維度中的地區數目而定。 如果所有摘要資料都已經預先計算為彙總，則查詢的回應時間僅會根據擷取指定資料格所需要的時間而定。 不需要計算或從事實資料表中讀取資料。  
  
 雖然預先計算 Cube 內所有可能的彙總可能會提供所有查詢的最快可能回應時間，但是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 可以輕鬆地從其他預先計算的彙總中計算出某些彙總值。 此外，計算所有可能的彙總需要大量處理時間和儲存體。 因此，在儲存需求與預先計算的可能彙總百分比之間會需要有所取捨。 如果未預先計算任何彙總 (0%)，則 Cube 所需的處理時間和儲存空間數量會減至最少，但是因為必須從分葉資料格中擷取回答每一個查詢所需的資料，然後在查詢時加以彙總來回答每一個查詢，所以查詢回應時間可能會變慢。 例如，傳回單一數字來回答前面所問的問題 (「1998 年西北地區 X 產品的銷售如何？」) 可能需要讀取數千個資料列，並擷取資料行的值 (此資料行是用來提供每個資料列的銷售量值)，然後計算總和。 此外，擷取該資料所需的時間長度可能會根據選擇的資料的儲存模式為 MOLAP、 HOLAP 或 ROLAP。  
  
## <a name="designing-aggregations"></a>設計彙總  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 納入了複雜的演算法，來選取預先計算的彙總，以便其他彙總可以快速地計算從預先計算的值。 例如，如果針對時間階層的月份層級預先計算出彙總，則季查詢的計算只需要加總三個數字，就可以視需要快速計算出來。 這個技巧可節省處理時間，並減少儲存需求，且對查詢回應時間的影響最小。  
  
 彙總設計精靈會提供選項讓您指定演算法的儲存體和百分比條件約束，以在查詢回應時間與儲存需求之間達成令人滿意的取捨。 不過，彙總設計精靈的演算法假設所有可能的查詢都同樣適合。 基於使用方式的最佳化精靈可讓您分析用戶端應用程式所提交的查詢，以調整量值群組的彙總設計。 使用這個精靈來微調 Cube 的彙總，即可增加常見查詢的回應能力，以及減少不常見之查詢的回應能力，而不會對 Cube 的儲存需求有太大影響。  
  
 雖然彙總是使用精靈所設計，但是除非已處理好所設計之彙總的資料分割，否則不會實際計算彙總。 建立彙總之後，如果 Cube 的結構變更，或是在 Cube 的來源資料表中加入或變更資料，則通常會需要檢閱 Cube 的彙總並再次處理該 Cube。  
  
## <a name="see-also"></a>另請參閱  
 [資料分割儲存模式及處理](partitions-partition-storage-modes-and-processing.md)  
  
  
