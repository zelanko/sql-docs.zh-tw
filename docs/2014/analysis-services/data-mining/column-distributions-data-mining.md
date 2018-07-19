---
title: 資料行散發 （資料採礦） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- normal distribution type [data mining]
- uniform distribution type [data mining]
- columns [data mining], distributions
- log normal distribution type [data mining]
- continuous columns
- distributions [data mining]
ms.assetid: 87e700de-32be-4bc8-b01d-ba4ee1ab48de
caps.latest.revision: 32
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6ee97f2b92aa1d98317ac9f420d6065340a60dba
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37189425"
---
# <a name="column-distributions-data-mining"></a>資料行散發 (資料採礦)
  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，您可以在採礦結構中定義資料行散發，以影響您建立採礦模型時演算法如何處理這些資料行中的資料。 針對某些演算法，若已知資料行包含值的通用散發，則在處理模型前先定義任何連續資料行的散發很有用。 如果您未定義散發，則產生之採礦模型所做出的預測，可能不如定義了散發的預測那般精確，因為演算法能用來解譯資料的資訊比較少。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中可用的演算法支援下列散發類型：  
  
 `Normal`  
 連續資料行的值形成含有一般分佈的長條圖。  
  
 ![使用常態分佈的長條圖](../media/normal-distribution.gif "常態分佈的長條圖")  
  
 `Log Normal`  
 連續資料行的值形成長條圖，其曲線在上端伸長，朝下端偏斜。  
  
 ![使用對數常態分佈的長條圖](../media/log-normal-distribution.gif "使用對數常態分佈的長條圖")  
  
 `Uniform`  
 連續資料行的值形成平坦曲線，其中所有值的機率都相當之。  
  
 ![使用統一分佈的長條圖](../media/uniform-distribution.gif "使用統一分佈的長條圖")  
  
 如需 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]提供的演算法的詳細資訊，請參閱[資料採礦演算法 &#40;Analysis Services - 資料採礦&#41;](data-mining-algorithms-analysis-services-data-mining.md)。  
  
## <a name="see-also"></a>另請參閱  
 [內容類型&#40;資料採礦&#41;](content-types-data-mining.md)   
 [採礦結構&#40;Analysis Services-資料採礦&#41;](mining-structures-analysis-services-data-mining.md)   
 [離散化方法&#40;資料採礦&#41;](discretization-methods-data-mining.md)   
 [散發套件&#40;DMX&#41;](/sql/dmx/distributions-dmx)   
 [採礦結構資料行](mining-structure-columns.md)  
  
  
