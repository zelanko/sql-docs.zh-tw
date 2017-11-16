---
title: "從採礦模型排除資料行 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- excluding mining model columns
- mining models [Analysis Services], columns
- columns [data mining], excluding
ms.assetid: 404fe5fe-3ba2-4b9b-8780-0d02343d467f
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a12584791ec8ea21a1338c09dbc0e5f7ef8f7a62
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="exclude-a-column-from-a-mining-model"></a>從採礦模型排除資料行
  當您建立新的採礦模型時，可能不想要使用模型做為基礎之採礦結構中已存在的所有資料行。 例如，您可能新增客戶名稱資料行用於鑽研，但不要將該資料行用於模型化。 或者，您可能決定為一個資料行建立具有不同離散化的多個複本，並且在每個模型中只使用其中一個複本，而忽略其餘複本。 您還可以選擇性地在多個不同模型中新增輸入資料行，檢查新增的變數如何影響輸出資料行。  
  
 您不需要為每個資料行組合都建立新的採礦結構，而是只需將資料行標示為不在特定的模型中使用。  
  
### <a name="to-exclude-a-column-from-a-mining-model"></a>若要從採礦模型排除資料行  
  
1.  在 **中之資料採礦設計師的** [採礦模型] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]索引標籤中，在適當的採礦模型之下，選取對應至您要排除之資料行的資料格。  
  
2.  從下拉式清單方塊中選取 [忽略]。  
  
## <a name="see-also"></a>另請參閱  
 [採礦模型工作和使用說明](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  

