---
title: 定義關聯性對話方塊 (Analysis Services-多維度資料) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.dimensionusage.definerelationship.f1
helpviewer_keywords:
- Define Relationship dialog box
ms.assetid: 0fcee7f1-f138-4c2e-ae8c-245395ee0fe8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2bc1ab86373fc7c3b4b32cdfdbc87f5d5dd4acf8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48196298"
---
# <a name="define-relationship-dialog-box-analysis-services---multidimensional-data"></a>定義關聯性對話方塊 (Analysis Services - 多維度資料)
  使用 **[定義關聯性]** 對話方塊，即可在 Cube 設計師中定義 Cube 維度和量值群組之間的關聯性。 在 Cube 設計師之 **[維度使用方式]** 索引標籤的 **[方格]** 窗格中，於資料格上按一下 **[...]** ，即可顯示 **[定義關聯性]** 對話方塊。  
  
## <a name="options"></a>選項。  
 **選取關聯性類型**  
 選取要在 Cube 維度和量值群組之間建立的維度關聯性類型。 選取維度關聯性類型會變更 **[詳細資料]** 窗格的內容。  
  
 如果選擇 **[無關聯性]** ，則不會建立維度關聯性。  
  
 **Detail**  
 顯示 [選取關聯性類型] 中，所選取維度關聯性類型的可用選項。  
  
## <a name="detail-pane-options"></a>詳細資料窗格選項  
 **[詳細資料]** 窗格會顯示下列選項，視 **[選取關聯性類型]** 中選取的關聯性類型而定：  
  
|關聯性類型|描述|選項|  
|-----------------------|-----------------|------------|  
|**沒有關聯性**|未定義關聯性，且 **[詳細資料]** 窗格不會顯示任何選項。||  
|**一般**|指定一般維度關聯性。 下列選項會顯示在 **[詳細資料]** 窗格中：|**資料粒度屬性**: <br />                      選取屬性，其中定義相對於維度之量值群組的資料粒度。 這個屬性通常是維度的索引鍵屬性。|  
|||**維度資料表**：顯示維度的主資料表。|  
|||**量值群組資料表**：顯示量值群組的事實資料表。|  
|||**關聯性**：顯示關聯性所依據之維度資料行和量值群組資料行的方格。 方格包含下列資料行：<br /><br /> **維度資料行**︰顯示與所選取資料粒度屬性相關的資料行。 注意：如果尚未產生維度，此選項會設定為 [產生] 。<br />**量值群組資料行**：<br />                              在量值群組中，選取與維度資料行相關的資料行。|  
|||**進階**：<br />                      按一下即可顯示 [量值群組繫結] 對話方塊，並在屬性和量值群組資料行之間的關聯性上編輯進階屬性，例如 Null 處理。 如需 [量值群組繫結] 對話方塊的詳細資訊，請參閱[量值群組繫結對話方塊 &#40;Analysis Services - 多維度資料&#41;](measure-group-bindings-dialog-box-analysis-services-multidimensional-data.md)。|  
|**事實**|指定事實維度關聯性。 下列選項會顯示在 **[詳細資料]** 窗格中：|**資料粒度屬性**：選取屬性，其中定義相對於維度之量值群組的資料粒度。 這個屬性通常是維度的索引鍵屬性。|  
|||**維度資料表**︰顯示主維度資料表。|  
|||**量值群組資料表**： <br />                      顯示量值群組所依據的資料表。|  
|**參考**|指定參考的維度關聯性。 下列選項會顯示在 **[詳細資料]** 窗格中：|**參考維度**: <br />                      顯示選取的維度。|  
|||**中繼維度**： <br />                      選取中繼維度。|  
|||**參考維度屬性**： <br />                      在參考維度中選取屬性，此屬性與 [中繼維度屬性] 中指定的中繼維度屬性有關。|  
|||**中繼維度屬性**： <br />                      在中繼維度中選取屬性，此屬性與 [參考維度] 中所指定參考維度的屬性有關。|  
|||**具體化**： <br />                      選取此選項即可將屬性成員儲存在中繼維度中，它會將參考維度中的屬性連結至 MOLAP 結構中的事實資料表。 將關聯性具體化是發揮最大查詢效能的預設行為，但代價是會增加處理時間和儲存空間。|  
|**多對多**|指定多對多維度關聯性。 下列選項會顯示在 **[詳細資料]** 窗格中：|**維度** ︰顯示選取的維度類型。|  
|||**中繼量值群組** ： <br />                      選取相關聯的中繼量值群組。<br /><br /> 注意：中繼量值群組至少必須有一個和所選取量值群組相同的維度。 此外，中繼量值群組和一般維度之間的關聯性資料粒度，必須大於或等於一般維度和所選取量值群組之間的資料粒度。|  
|**資料採礦**|指定資料採礦維度關聯性。 下列選項會顯示在 **[詳細資料]** 窗格中：|**目標維度**︰顯示選取的資料採礦維度。<br /><br /> 注意：您必須選取資料採礦維度，才能建立資料採礦維度關聯性。|  
|||**來源維度**︰選取由資料採礦維度提供預測分析的維度。|  
  
## <a name="see-also"></a>另請參閱  
 [維度關聯性](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)   
 [維度使用方式&#40;Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](dimension-usage-cube-designer-analysis-services-multidimensional-data.md)   
 [Analysis Services Designers and Dialog Boxes&#40;多維度資料&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)  
  
  
