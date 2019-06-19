---
title: 指定資料行對應對話方塊 （採礦精確度圖表） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.accuracychart.coltotablecolmapping.f1
ms.assetid: 68e9e2d2-173f-4363-a515-fc60bfee3af0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4416a51ea32500d56c209d745065da20bf8010c9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66068414"
---
# <a name="specify-column-mapping-dialog-box-mining-accuracy-chart"></a>指定資料行對應對話方塊 (採礦精確度圖表)
  使用 [指定資料行對應]  索引標籤可從外部資料來源選取資料表，並且將資料行對應至資料採礦模型。 接著您就可以使用該外部資料來測試採礦模型的精確度，並將結果顯示在精確度圖表中。  
  
 **如需詳細資訊：＜＞**[測試及驗證 &#40;資料採礦&#41;](data-mining/testing-and-validation-data-mining.md)  
  
## <a name="options"></a>選項  
 **採礦結構**  
 顯示選取的採礦結構，其中包含您要測試的模型。  
  
 **選取結構**  
 按一下即可開啟 [選取採礦結構]  對話方塊，然後選取不同的採礦結構。  
  
 **選取輸入的資料表**  
 顯示用來產生增益圖的選取之輸入資料表。 選取其中包含將用來測試模型精確度之測試資料的資料表。  
  
> [!NOTE]  
>  如果窗格不包含任何資料表，請按一下 [選取案例資料表]  以從資料來源檢視新增資料表。  
  
 **移除資料表**  
 移除選取的資料表。 如果尚未選取資料表，或在 [選取輸入資料表]  清單中未顯示任何資料表，則此按鈕會停用。  
  
 **選取案例資料表**  
 按一下即可開啟 [選取資料表]  對話方塊，並選取資料來源檢視。  
  
 **注意**：只有當未選取案例資料表時，才會顯示這個按鈕。 若要啟用按鈕而使您可以選取不同的案例資料表，請選取所有現有的資料表，然後再按一下 [移除資料表]  。  
  
 **選取巢狀的資料表**  
 開啟 [選取資料表]  對話方塊。 唯有選取了案例資料表時，才會顯示這個按鈕。 如果關聯的採礦結構未包含巢狀資料表，這個按鈕就會停用。  
  
 **修改聯結**  
 開啟 [指定巢狀聯結]  對話方塊。 唯有選取了巢狀資料表時，才可以使用此按鈕。  
  
## <a name="see-also"></a>另請參閱  
 [測試及驗證工作與操作方法&#40;資料採礦&#41;](data-mining/testing-and-validation-tasks-and-how-tos-data-mining.md)   
 [採礦精確度圖表設計師&#40;資料採礦&#41;](mining-accuracy-chart-designer-data-mining.md)  
  
  
