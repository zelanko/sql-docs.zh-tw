---
title: 篩選對話方塊 （採礦精確度圖表） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 71e884a9-7ec4-4459-a4c4-87f6c796d478
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 554c7c0f375d63710c86e37666ee98c6dac6daf6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66081166"
---
# <a name="filter-dialog-box-mining-accuracy-chart"></a>篩選對話方塊 (採礦精確度圖表)
  [篩選]  對話方塊會幫助您建立可套用至資料集的條件。 此資料集可以是用於測試的外部資料集，或是用於定型採礦模型的案例資料。 此對話方塊可幫助您建立準則，您可以在 [資料集篩選器]  對話方塊或 [模型篩選器]  對話方塊中，將這些準則儲存為更複雜之篩選準則的一部分。  
  
-   [資料集篩選器]  對話方塊可從 [採礦精確度圖表]  設計工具的 [輸入選擇]  索引標籤中存取。  
  
-   [模型篩選器]  對話方塊可從 [資料採礦] 設計工具的 [採礦模型]  索引標籤中存取。  
  
 如果您要將篩選套用到採礦模型，請先使用 [模型篩選器]  對話方塊來選擇資料表。 然後，您可以使用 [篩選]  對話方塊，建立只套用至該資料表的條件。  
  
 如果您要建立可套用至外部測試資料集的篩選，請先使用 [資料集篩選器]  對話方塊，從資料來源檢視中的資料表清單選擇資料表。 然後，您可以使用 [篩選]  對話方塊，建立只套用至該資料表的條件。  
  
 在建立套用至單一資料表的一組條件之後，[!INCLUDE[clickOK](../includes/clickok-md.md)]。 您在 [篩選]  對話方塊中所做的變更會自動加入上層對話方塊 ([資料集篩選器]  或 [模型篩選器]  ) 中的篩選運算式。  
  
 如果您將篩選套用至新的資料集，則只會使用現有的資料採礦模型來評估資料集中符合條件的案例。 但是，如果要將篩選套用至採礦模型本身，則只會針對採礦模型中符合這些準則的案例來評估模型的精確度。  
  
 **如需詳細資訊：＜＞**[測試及驗證 &#40;資料採礦&#41;](data-mining/testing-and-validation-data-mining.md)  
  
## <a name="options"></a>選項  
 **條件**  
 包含資料行的方格，您會在這裡根據 [資料集篩選器]  對話方塊中選取的資料表指定資料行的條件。  
  
|值|描述|  
|-----------|-----------------|  
|**及/或**|按一下此選項，指定是要將 AND 運算子還是 OR 運算子套用到這一行的條件。 只有當您從 [採礦結構資料行]  清單中選取資料行之後，才可以使用這些值。|  
|**採礦結構資料行**|按一下此選項，從資料表中包含的資料行清單選取資料行，此資料表是您從 [資料集篩選器]  對話方塊中的資料來源選取而來。|  
|**運算子**|從清單選取運算子。 可用的運算子取決於資料行的資料類型而定。<br /><br /> 如果此資料行包含離散值，則只能使用下列運算子：<br /><br /> = (equal to)、<> (不等於)、IS NOT NULL、IS NULL。<br /><br /> 如果此資料行包含連續值，則也支援大於的運算子和小於運算。|  
|**值**|輸入當做條件使用的值。|  
  
## <a name="see-also"></a>另請參閱  
 [測試及驗證工作與操作方法&#40;資料採礦&#41;](data-mining/testing-and-validation-tasks-and-how-tos-data-mining.md)   
 [採礦精確度圖表設計師&#40;資料採礦&#41;](mining-accuracy-chart-designer-data-mining.md)  
  
  
