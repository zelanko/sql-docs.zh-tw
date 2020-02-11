---
title: 配量來源 Cube （資料採礦嚮導） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.dmwizard.slicesourcecube.f1
ms.assetid: 16485608-d3b9-49ee-8baa-948038cdd7ec
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bcb156d5c0a3c1332e748878ddebda1772b80696
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66068600"
---
# <a name="slice-source-cube-data-mining-wizard"></a>配量來源 Cube (資料採礦精靈)
  
  **
  ** 您可以使用 [配量來源 Cube] 對話方塊來限制用於培訓模型的資料。 Cube 通常包含了與許多不同維度及屬性相關的資料，例如所有商店、所有區域和所有產品。 根據無限制的屬性組合來培訓模型並不實用，所以您要使用此對話方塊選擇用於培訓模型的一組特定項目。  
  
 例如，針對 AdventureWorks Cube，您可能會依特定產品線、地區或年份配量，以取得一部分的資料。  
  
 如果您不熟悉配量和 Cube，建議您檢閱這些文章：  
  
-   [將分割區配量屬性設定 &#40;Analysis Services&#41;](multidimensional-models/set-the-partition-slice-property-analysis-services.md)  
  
-   [建立和管理本機資料分割 &#40;Analysis Services&#41;](multidimensional-models/create-and-manage-a-local-partition-analysis-services.md)  
  
> [!NOTE]  
>  請注意，資料分割的 Slice 屬性不支援動態多維度運算式 (MDX) 函數 (例如 [Generate &#40;MDX&#41;](/sql/mdx/generate-mdx) 或 [Except &#40;MDX&#41;](/sql/mdx/except-mdx-function))。 您必須使用明確的 Tuple 或成員參考來定義配量。  
>   
>  例如，您必須依特定年份列舉每個成員，而不是使用[： &#40;範圍&#41; &#40;MDX&#41;](/sql/mdx/range-mdx)來定義範圍。  
>   
>  如果您需要定義複雜的配量，我們建議您使用 XMLA Alter 指令碼在配量中定義 Tuple。 然後在處理資料分割區之前，您可以使用 ascmd 命令列工具或 SSIS [Analysis Services Execute DDL Task](../integration-services/control-flow/analysis-services-execute-ddl-task.md) 立即執行該指令碼並建立指定集合的成員。  
  
 **如需詳細資訊：** [資料採礦 Wizard &#40;Analysis Services 資料採礦&#41;](data-mining/data-mining-wizard-analysis-services-data-mining.md)，請[建立關聯式的採礦結構](data-mining/create-a-relational-mining-structure.md)  
  
## <a name="options"></a>選項。  
 **維度**  
 選取您要配量的維度。  
  
 **階層**  
 選取您要配量的階層。 您可以選擇階層的任一層級，但是模型中所用的屬性將只拘限於您自選的層級。  
  
 例如，假設您選擇 Geography 階層並且選取 Country 當做層級，便無法建立使用 City 做為屬性的模型。 相對地，若是選擇了 City 做為要配量的階層層級，您就無法建立以 Country 為根據的採礦模型。  
  
 **運算子**  
 選取要用於建立配量運算式的運算子。  
  
 例如，如果您選擇 [Geography] 做為階層，則可以選取 [運算子 =]，然後輸入 "歐洲" 作為篩選準則，僅取得歐洲的 cube 資料。  
  
 **篩選運算式**  
 輸入根據選取的維度篩選 Cube 時要當做準則使用的運算式。  
  
 **參數**  
 此選項不適用於資料採礦模型。  
  
## <a name="see-also"></a>另請參閱  
 [正在完成 Wizard &#40;資料採礦嚮導&#41;](completing-the-wizard-data-mining-wizard.md)   
 [資料採礦嚮導 F1 說明 &#40;Analysis Services-資料採礦&#41;](data-mining-wizard-f1-help-analysis-services-data-mining.md)   
 [指定 &#40;資料採礦嚮導&#41;的「採礦模型資料行使用方式」](specify-mining-model-column-usage-data-mining-wizard.md)  
  
  
