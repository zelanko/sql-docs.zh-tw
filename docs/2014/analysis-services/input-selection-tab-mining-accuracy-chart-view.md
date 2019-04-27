---
title: 輸入選取範圍索引標籤 （採礦精確度圖表檢視） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.accuracychart.columnmapping.f1
ms.assetid: f8b1193c-5c86-4c7e-8e35-158d293184fa
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c1027310bdf012f00e7b70981521088d69d08598
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62729890"
---
# <a name="input-selection-tab-mining-accuracy-chart-view"></a>輸入選取範圍索引標籤 (採礦精確度圖表檢視)
  使用 [採礦精確度圖表] 設計師的 [輸入選擇] 索引標籤可以指定用於測試模型及建立精確度圖表的資料來源。  
  
 **如需詳細資訊：＜＞**[測試及驗證 &#40;資料採礦&#41;](data-mining/testing-and-validation-data-mining.md)  
  
## <a name="options"></a>選項。  
 **同步處理預測****資料行和值**  
 選取即可協調方格中的可預測屬性，使得即使它們具有不同的名稱，仍會在模型定型期間，從相同可預測採礦結構資料行中衍生而來。  
  
 **注意** ：預設會選取此選項。 唯有在知道兩個採礦結構資料行都衍生自相同的基礎關聯式或多維度來源的情況下，以及這些資料行具有相同的狀態或分隔的情況下，才應清除此方塊。  
  
 **選取可預測的採礦模型資料行，以顯示在增益圖**  
 方格包含用來控制將哪些模型包含在增益圖中，以及增益圖如何使用它們的資料行。  
  
|值|描述|  
|-----------|-----------------|  
|**顯示**|在要顯示在圖表中的採礦模型中，選取每個可預測資料行名稱旁的方塊。<br /><br /> 如果圖表過於複雜而無法輕鬆檢視，請清除一或多個資料行旁的方塊以簡化圖表。<br /><br /> 注意:您無法建立精確度圖表，除非已選取至少一個資料行。|  
|**採礦模型**|列出採礦結構內所包含的採礦模型。|  
|**可預測資料行名稱**|選取採礦模型內所包含之用來建立增益圖的可預測資料行。|  
|**預測值**|選取可預測資料行的值。 如果您將此保留空白，增益圖就會針對可預測資料行的所有狀態，預測模型的執行效益。|  
  
 **選取要用於精確度圖表的資料集**  
 包含用來指定精確度測試資料之三個選項的選項群組。  
  
|值|描述|  
|-----------|-----------------|  
|**使用採礦模型測試案例**|使用在對採礦結構進行資料分割時所建立的測試集，並套用定義於模型的篩選。 如需模型篩選的相關資訊，請參閱 [Filters for Mining Models &#40;Analysis Services - Data Mining&#41;](data-mining/mining-models-analysis-services-data-mining.md)|  
|**使用採礦結構測試案例**|使用在對採礦結構進行資料分割時所建立的測試集。|  
|**指定不同的資料集**|從現有的資料來源檢視指定用來當做測試資料集的資料表。|  
  
## <a name="filtering-options"></a>篩選選項  
 如果選取 [指定不同的資料集] 選項，就可以定義資料來源檢視並建立套用至該資料的篩選。 在建立篩選時，您是在查詢中建立會從資料來源檢視傳回測試資料的 WHERE 子句。  
  
 **注意**：您無法使用 [輸入選擇] 索引標籤在採礦模型上指定篩選。若要建立模型篩選，請按一下 [採礦模型] 索引標籤，然後編輯模型屬性。  
  
 如果沒有建立鑑效組集來測試何時建立了採礦結構，則可以選取此選項，然後將原始資料來源檢視指定為測試集。 您也可以使用這個解決方法在原始資料集上設定篩選。  
  
 **指定資料行對應**  
 開啟 [指定資料行對應] 對話方塊，您可從中選取資料來源、指定案例及巢狀資料表，並且將外部資料行對應至採礦結構資料行。  
  
 如需詳細資訊，請參閱[指定資料行對應對話方塊 &#40;採礦精確度圖表&#41;](specify-column-mapping-dialog-box-mining-accuracy-chart.md)。  
  
 **篩選運算式**  
 顯示使用篩選編輯器所建立的篩選條件。  
  
 **開啟篩選編輯器**  
 開啟 [資料集篩選器] 對話方塊 (可用來選取外部資料表，並在案例資料表資料行上設定條件) 及 [篩選] 對話方塊 (可協助您建立條件以套用至選取的資料表中的個別資料行或巢狀資料表中的資料行)。  
  
## <a name="see-also"></a>另請參閱  
 [測試及驗證工作與操作方法&#40;資料採礦&#41;](data-mining/testing-and-validation-tasks-and-how-tos-data-mining.md)   
 [採礦精確度圖表設計師&#40;資料採礦&#41;](mining-accuracy-chart-designer-data-mining.md)   
 [將篩選套用至採礦模型](data-mining/apply-a-filter-to-a-mining-model.md)   
 [採礦模型的篩選 &#40;Analysis Services - 資料採礦&#41;](data-mining/mining-models-analysis-services-data-mining.md)  
  
  
