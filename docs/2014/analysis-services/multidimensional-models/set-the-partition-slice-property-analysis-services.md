---
title: 設定 Partition Slice 屬性 (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 08/05/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- partitions [Analysis Services], data slices
- data slices [Analysis Services]
ms.assetid: 507b91e5-7f85-4c22-be97-4d7a676e6667
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c94ac9865540016020bf1853bc318881defdaea7
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53374060"
---
# <a name="set-the-partition-slice-property-analysis-services"></a>設定 Partition Slice 屬性 (Analysis Services)
  資料配量是協助將查詢導向到適當之分割區資料的重要最佳化功能。 明確設定 Slice 屬性可提升查詢效能，方法是覆寫 MOLAP and HOLAP 分割區所產生的預設配量。 此外，Slice 屬性可在處理分割區時，提供額外的驗證檢查。  
  
 您可以在建立分割區之後但在處理分割區之前，使用 Slice 屬性指定資料配量。 在 [分割區] 索引標籤上，展開量值群組，然後以滑鼠右鍵按一下分割區並選取 **[屬性]**。  
  
## <a name="defining-a-slice"></a>定義配量  
 Slice 屬性的有效值為 MDX 成員、集合或 Tuple。 下列範例說明有效的配量語法：  
  
|配量|成員、集合或 Tuple|  
|-----------|--------------------------|  
|[Date].[Calendar].[Calendar Year].&[2010]|在分割區上指定此配量，以包含 2010 年的事實 (假設模型包含日曆年度階層的日期維度，其中 2010 是成員)。 雖然分割區來源 WHERE 子句或資料表可能已依 2010 篩選，指定配量可在處理期間提供額外檢查，並在查詢執行期間提供更鎖定目標的掃描。|  
|{ [Sales Territory].[Sales Territory Country].&[Australia], [Sales Territory].[Sales Territory Country].&[Canada] }|在分割區上指定此配量，以包含銷售領域資訊的事實。 配量可以是由兩個或多個成員組成的 MDX 集合。|  
|[Measures].[Sales Amount Quota] > '5000'|此配量顯示 MDX 運算式。|  
  
 分割區的資料配量應該儘量反映分割區中的資料。 例如，若分割區限制為 2012 資料，則分割區的資料配量應該指定 Time 維度的 2012 成員。 您不一定能夠指定會反映分割區確切內容的資料配量。 例如，若分割區只包含 1 月和 2 月的資料，但 Time 維度的層級為年、季和月，則分割區精靈無法同時選取 1 月和 2 月的成員。 在此情況下，請選取能反映分割區內容之成員的父系。 在這個範例中，請選取第 1 季。  
  
 如需資料配量優點的說明，請參閱＜ [在 SSAS Cube 分割區上設定配量](https://go.microsoft.com/fwlink/?LinkId=317783)＞。  
  
> [!NOTE]  
>  請注意，資料分割的 Slice 屬性不支援動態多維度運算式 (MDX) 函數 (例如 [Generate &#40;MDX&#41;](/sql/mdx/generate-mdx) 或 [Except &#40;MDX&#41;](/sql/mdx/except-mdx-function))。 您必須使用明確的 Tuple 或成員參考來定義配量。  
>   
>  比方說，而不是使用[:&#40;範圍&#41; &#40;MDX&#41; ](/sql/mdx/range-mdx)函式來定義範圍，您需要以特定的年份來列舉每個成員。  
>   
>  如果您需要定義複雜的配量，我們建議您使用 XMLA Alter 指令碼在配量中定義 Tuple。 然後在處理資料分割區之前，您可以使用 ascmd 命令列工具或 SSIS [Analysis Services Execute DDL Task](../../integration-services/control-flow/analysis-services-execute-ddl-task.md) 工作立即執行該指令碼並建立指定集合的成員。  
  
## <a name="see-also"></a>另請參閱  
 [建立及管理本機資料分割 &#40;Analysis Services&#41;](create-and-manage-a-local-partition-analysis-services.md)  
  
  
