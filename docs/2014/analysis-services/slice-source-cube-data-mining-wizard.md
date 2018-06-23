---
title: 配量來源 Cube （資料採礦精靈） |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dm.dmwizard.slicesourcecube.f1
ms.assetid: 16485608-d3b9-49ee-8baa-948038cdd7ec
caps.latest.revision: 23
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: a0e3badd385e654db3b869a197130fde26fbffcc
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36132732"
---
# <a name="slice-source-cube-data-mining-wizard"></a>配量來源 Cube (資料採礦精靈)
   您可以使用 [配量來源 Cube] 對話方塊來限制用於培訓模型的資料。 Cube 通常包含了與許多不同維度及屬性相關的資料，例如所有商店、所有區域和所有產品。 根據無限制的屬性組合來培訓模型並不實用，所以您要使用此對話方塊選擇用於培訓模型的一組特定項目。  
  
 例如，針對 AdventureWorks Cube，您可能會依特定產品線、地區或年份配量，以取得一部分的資料。  
  
 如果您不熟悉配量和 Cube，建議您檢閱這些文章：  
  
-   [設定 Partition Slice 屬性&#40;Analysis Services&#41;](multidimensional-models/set-the-partition-slice-property-analysis-services.md)  
  
-   [建立及管理本機資料分割&#40;Analysis Services&#41;](multidimensional-models/create-and-manage-a-local-partition-analysis-services.md)  
  
> [!NOTE]  
>  請注意，資料分割的 Slice 屬性不支援動態多維度運算式 (MDX) 函數 (例如 [Generate &#40;MDX&#41;](/sql/mdx/generate-mdx) 或 [Except &#40;MDX&#41;](/sql/mdx/except-mdx-function))。 您必須使用明確的 Tuple 或成員參考來定義配量。  
>   
>  例如，而不是使用[:&#40;範圍&#41; &#40;MDX&#41; ](/sql/mdx/range-mdx)定義的範圍，您必須以特定的年份來列舉每個成員。  
>   
>  如果您需要定義複雜的配量，我們建議您使用 XMLA Alter 指令碼在配量中定義 Tuple。 然後，您可以使用 ascmd 命令列工具或 SSIS [Analysis Services 執行 DDL 工作](../integration-services/control-flow/analysis-services-execute-ddl-task.md)執行指令碼，並在處理分割區之前，立即建立指定的集合的成員。  
  
 **如需詳細資訊，請參閱**[資料採礦精靈 &#40;Analysis Services - 資料採礦&#41;](data-mining/data-mining-wizard-analysis-services-data-mining.md)、[建立關聯式採礦結構](data-mining/create-a-relational-mining-structure.md)  
  
## <a name="options"></a>選項。  
 **Dimension**  
 選取您要配量的維度。  
  
 **Hierarchy**  
 選取您要配量的階層。 您可以選擇階層的任一層級，但是模型中所用的屬性將只拘限於您自選的層級。  
  
 例如，假設您選擇 Geography 階層並且選取 Country 當做層級，便無法建立使用 City 做為屬性的模型。 相對地，若是選擇了 City 做為要配量的階層層級，您就無法建立以 Country 為根據的採礦模型。  
  
 **[運算子]**  
 選取要用於建立配量運算式的運算子。  
  
 例如，若您選擇了 Geography 做為階層，即可選取運算子 = 再接著輸入 "Europe" 當做篩選，從而取得只限 Europe 地區的 Cube 資料。  
  
 **篩選運算式**  
 輸入根據選取的維度篩選 Cube 時要當做準則使用的運算式。  
  
 **參數**  
 此選項不適用於資料採礦模型。  
  
## <a name="see-also"></a>另請參閱  
 [正在完成精靈&#40;資料採礦精靈&#41;](completing-the-wizard-data-mining-wizard.md)   
 [資料採礦精靈 F1 說明&#40;Analysis Services-資料採礦&#41;](data-mining-wizard-f1-help-analysis-services-data-mining.md)   
 [指定採礦模型資料行使用方式&#40;資料採礦精靈&#41;](specify-mining-model-column-usage-data-mining-wizard.md)  
  
  
