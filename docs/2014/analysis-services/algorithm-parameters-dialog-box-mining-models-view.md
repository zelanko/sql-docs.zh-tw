---
title: 演算法參數對話方塊 （採礦模型檢視） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.models.algorithmparameters.f1
helpviewer_keywords:
- Algorithm Parameters dialog box
ms.assetid: 57f9f6f8-8ca4-4a6e-8f18-85f0571b7060
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c72a3c52da21ca7af10103010500bb43fd46a10a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66062605"
---
# <a name="algorithm-parameters-dialog-box-mining-models-view"></a>演算法參數對話方塊 (採礦模型檢視)
  使用 [演算法參數]  對話方塊，即可調整所選取模型特定的演算法參數。 當您變更演算法參數時，您通常會變更採礦模型的結果。 每一個參數影響結果的方式取決於您所使用的演算法和資料而定。 如需詳細資訊，請參閱[自訂採礦模型和結構](data-mining/customize-mining-models-and-structure.md)。  
  
## <a name="options"></a>選項。  
 **參數**  
 列出所選取採礦模型可以使用的參數。  
  
 下列清單描述可用的資料行。  
  
|「資料行」|描述|  
|------------|-----------------|  
|**參數**|列出參數的名稱。|  
|**值**|只有當您要變更參數的預設值時，才輸入值。|  
|**預設值**|如果您在 [值]  資料行中並未提供值，則會列出演算法使用之參數的預設值。|  
|**Range**|列出可以輸入到 [值]  資料行之可能值的範圍。 範圍可以是下列其中一項：<br /><br /> 分隔的清單，例如 1、 2、 3<br /><br /> 一個內含範圍，例如 [0，100]<br /><br /> 排除範圍，例如 (0，...)<br /><br /> 組合，例如 [0，...)|  
  
 **說明**  
 描述 [參數]  清單中選取的參數。  
  
 **[加入]**  
 按一下此選項，可將其他演算法特定的參數加入至清單中。 加入參數之後，您可以在 [參數]  資料行中輸入正確的名稱，並提供 [值]  資料行中的值。  
  
 **移除**  
 按一下此選項，可從清單中刪除自訂參數。  
  
 如果您從清單中刪除其中一個標準 Analysis Services 演算法參數，此參數仍然會在模型中使用，但是將會使用該參數的預設值。 此參數不會永久刪除，而且下次當您開啟對話方塊時就會出現。  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦演算法 &#40;Analysis Services - 資料採礦&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [採礦模型檢視&#40;資料採礦模型設計工具&#41;](mining-models-view-data-mining-model-designer.md)   
 [移動資料採礦物件](data-mining/moving-data-mining-objects.md)  
  
  
