---
title: 資料類型 （資料採礦） |Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4b62c9a4ebc9caf9875a1e5b6aef987bf0b4fa8a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "68183360"
---
# <a name="data-types-data-mining"></a>資料類型 (資料採礦)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  當您在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中建立採礦模型或採礦結構時，您必須針對採礦結構內的每一個資料行定義資料類型。 此資料類型會告訴分析引擎，資料來源中的資料是數值還是文字，以及應該如何處理資料。 例如，如果您的來源資料包含數值資料，您可以指定數字應該視為整數還是使用小數位數。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支援以下採礦結構資料行的資料類型：  
  
|資料類型|支援的內容類型|  
|---------------|-----------------------------|  
|**Text**|Cyclical、Discrete、Discretized、Key Sequence、Ordered、Sequence|  
|**長整數**|Continuous、Cyclical、Discrete、Discretized、Key、Key Sequence、Key Time、Ordered、Sequence、Time<br /><br /> Classified|  
|**布林**|Cyclical、Discrete、Ordered|  
|**Double**|Continuous、Cyclical、Discrete、Discretized、Key、Key Sequence、Key Time、Ordered、Sequence、Time<br /><br /> Classified|  
|**日期**|Continuous、Cyclical、Discrete、Discretized、Key、Key Sequence、Key Time、Ordered|  
  
> [!NOTE]  
>  只有協力廠商演算法才支援 Time 和 Sequence 內容類型。 系統支援 Cyclical 和 Ordered 內容類型，但是大部分的演算法將它們視為離散值，因此不會執行特殊處理。  
  
 此資料表也會顯示每種資料類型所支援的「內容類型」  。  
  
 此內容類型是資料採礦特有的，可讓您自訂在採礦模型中處理或計算資料的方式。 例如，即使您的資料行包含數字，您還是可能需要建立它們的模組以作為離散值。 如果資料行包含數字，您也可以指定它們是分類收納或離散化，或指定模型將它們處理為連續值。 因此，內容類型會對模型造成巨大影響。 如需所有內容類型的清單，請參閱 [內容類型 &#40;資料採礦&#41;](../../analysis-services/data-mining/content-types-data-mining.md)。  
  
> [!NOTE]  
>  在其他機器學習系統中，您可能會遇到「名義資料」  、「因素」  或「類別」  、「序數資料」  或「序列資料」  這些術語。 一般而言，這些會對應到內容類型。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，資料類型只會指定儲存體的實值類型，而不是它在模型中的使用方式。  
  
## <a name="specifying-a-data-type"></a>指定資料類型  
 如果您使用資料採礦延伸模組 (DMX) 直接建立採礦模型，當您定義此模型時，可以針對每一個資料行定義資料類型，而且 Analysis Services 將會同時建立具有指定之資料類型的對應採礦結構。 如果您使用精靈建立採礦模型或採礦結構，Analysis Services 將會建議一個資料類型，或者，您也可以從清單中選擇資料類型。  
  
## <a name="changing-a-data-type"></a>變更資料類型  
 如果您變更資料行的資料類型，一定要重新處理採礦結構及根據該結構的任何採礦模型。 有時當您變更資料類型時，該資料行就不能再用於特定的模型中。 在這種情況下，當您重新處理模型時，Analysis Services 將會引發錯誤，或是處理此模型，但是不處理該特定資料行。  
  
## <a name="see-also"></a>另請參閱  
 [內容類型 &#40;資料採礦&#41;](../../analysis-services/data-mining/content-types-data-mining.md)   
 [內容類型 &#40;DMX&#41;](../../dmx/content-types-dmx.md)   
 [資料採礦演算法 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [採礦結構 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [資料類型 &#40;DMX&#41;](../../dmx/data-types-dmx.md)   
 [採礦模型資料行](../../analysis-services/data-mining/mining-model-columns.md)   
 [採礦結構資料行](../../analysis-services/data-mining/mining-structure-columns.md)  
  
  
