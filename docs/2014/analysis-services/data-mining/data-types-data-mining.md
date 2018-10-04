---
title: 資料類型 （資料採礦） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data types [data mining]
- columns [data mining], data types
- data mining [Analysis Services], data types
ms.assetid: 4af5b7db-790b-459c-b2b4-00f0cf6b5ce4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 77a0c6f2f0100e7e0c0e73ee70bc8705135d259f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48225248"
---
# <a name="data-types-data-mining"></a>資料類型 (資料採礦)
  當您在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中建立採礦模型或採礦結構時，您必須針對採礦結構內的每一個資料行定義資料類型。 此資料類型會告訴資料採礦引擎，資料來源中的資料是數值還是文字，以及應該如何處理資料。 例如，如果您的來源資料包含數值資料，您可以指定數字應該視為整數還是使用小數位數。  
  
 每一個資料類型都會支援一個或多個內容類型。 藉由設定內容類型，您可以自訂處理資料行資料的方式或是計算採礦模型資料的方式。  
  
 例如，如果您在資料行中有數值資料，您可以選擇將資料當做數值或文字資料類型來處理。 如果您選擇數值資料類型，您可以設定幾種不同的內容類型：您可以離散化數字，或是將數字當做連續值來處理。 如需所有內容類型的清單，請參閱[內容類型 &#40;資料採礦&#41;](content-types-data-mining.md)。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支援以下採礦結構資料行的資料類型：  
  
|資料類型|支援的內容類型|  
|---------------|-----------------------------|  
|`Text`|Cyclical、Discrete、Discretized、Key Sequence、Ordered、Sequence|  
|`Long`|Continuous、Cyclical、Discrete、Discretized、Key、Key Sequence、Key Time、Ordered、Sequence、Time<br /><br /> Classified|  
|`Boolean`|Cyclical、Discrete、Ordered|  
|`Double`|Continuous、Cyclical、Discrete、Discretized、Key、Key Sequence、Key Time、Ordered、Sequence、Time<br /><br /> Classified|  
|`Date`|Continuous、Cyclical、Discrete、Discretized、Key、Key Sequence、Key Time、Ordered|  
  
> [!NOTE]  
>  只有協力廠商演算法才支援 Time 和 Sequence 內容類型。 系統支援 Cyclical 和 Ordered 內容類型，但是大部分的演算法將它們視為離散值，因此不會執行特殊處理。  
  
## <a name="specifying-a-data-type"></a>指定資料類型  
 如果您使用資料採礦延伸模組 (DMX) 直接建立採礦模型，當您定義此模型時，可以針對每一個資料行定義資料類型，而且 Analysis Services 將會同時建立具有指定之資料類型的對應採礦結構。 如果您使用精靈建立採礦模型或採礦結構，Analysis Services 將會建議一個資料類型，或者，您也可以從清單中選擇資料類型。  
  
## <a name="changing-a-data-type"></a>變更資料類型  
 如果您變更資料行的資料類型，一定要重新處理採礦結構及根據該結構的任何採礦模型。 有時當您變更資料類型時，該資料行就不能再用於特定的模型中。 在這種情況下，當您重新處理模型時，Analysis Services 將會引發錯誤，或是處理此模型，但是不處理該特定資料行。  
  
## <a name="see-also"></a>另請參閱  
 [內容類型&#40;資料採礦&#41;](content-types-data-mining.md)   
 [內容類型&#40;DMX&#41;](/sql/dmx/content-types-dmx)   
 [資料採礦演算法&#40;Analysis Services-資料採礦&#41;](data-mining-algorithms-analysis-services-data-mining.md)   
 [採礦結構&#40;Analysis Services-資料採礦&#41;](mining-structures-analysis-services-data-mining.md)   
 [資料型別&#40;DMX&#41;](/sql/dmx/data-types-dmx)   
 [採礦模型資料行](mining-model-columns.md)   
 [採礦結構資料行](mining-structure-columns.md)  
  
  
