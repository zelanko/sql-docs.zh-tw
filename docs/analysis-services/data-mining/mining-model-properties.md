---
title: 採礦模型屬性 |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8ba834b497950357b83a4ec052654b5a4998b928
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34015805"
---
# <a name="mining-model-properties"></a>採礦模型屬性
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  採礦模型具有以下種類的屬性：  
  
-   繼承自採礦結構的屬性，這些屬性可定義此模型所使用之資料的資料類型和內容類型。  
  
-   與用來建立採礦模型之演算法相關的屬性，包括任何客戶參數。  
  
-   在模型上定義篩選的屬性，可用來定型模型。  
  
 採礦模型的屬性一開始是在您建立模型時所定義；但是，您之後可以更改大多數的屬性，包括演算法參數、篩選以及資料行使用方式屬性。 您可藉由使用資料採礦設計師的 [採礦模型] 索引標籤或使用 AMO 或 XMLA 來變更屬性。  
  
 每當您變更模型的任何屬性時，您都必須重新處理模型，才能在模型中反映變更。 即使變更只牽涉到中繼資料 (例如資料行別名或描述)，也需要重新處理。  
  
## <a name="properties-of-models"></a>模型的屬性  
 下表描述採礦模型特有的屬性。 此外，也有一些屬性可以在採礦的個別資料行中設定。  
  
|屬性|說明|  
|--------------|-----------------|  
|**演算法**|設定採礦模型的演算法類型。|  
|**AlgorithmParameters**|設定每一種演算法類型可用的演算法參數的值。|  
|**篩選**|設定篩選以套用至用於培訓及測試採礦模型的資料。 篩選定義會與模型一起儲存，並在建立預測查詢或測試模型正確性時選擇性地使用。<br /><br /> 在培訓模型時，模型篩選並非選擇性的。|  
|**名稱**|設定採礦模型的名稱。|  
|**AllowDrillThrough**|指定採礦模型上是否啟用鑽研。|  
  
## <a name="properties-of-model-columns"></a>模型資料行的屬性  
 針對採礦模型中的每一個資料行，您可以設定下列資料採礦特有的屬性。 針對採礦結構中的每一個採礦模型，您可以將這些屬性設定為不同的值。  
  
|屬性|說明|  
|--------------|-----------------|  
|**說明**|描述採礦資料行的目的。|  
|**名稱**|設定採礦模型資料行的名稱。 您可以輸入新名稱，為採礦模型資料行提供別名。|  
|**ModelingFlags**|設定資料行的任何演算法特定旗標。|  
|**SourceColumnID**|代表模型資料行所依據之採礦結構資料行的名稱。<br /><br /> 此屬性是唯讀的。|  
|**使用方式**|設定採礦模型如何使用資料行。|  
  
## <a name="see-also"></a>另請參閱  
 [採礦模型資料行](../../analysis-services/data-mining/mining-model-columns.md)   
 [採礦結構 & #40;Analysis Services-資料採礦 & #41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [採礦模型的工作與操作方法](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [變更採礦模型的屬性](../../analysis-services/data-mining/change-the-properties-of-a-mining-model.md)   
 [資料採礦工具](../../analysis-services/data-mining/data-mining-tools.md)   
 [建立關聯式採礦結構](../../analysis-services/data-mining/create-a-relational-mining-structure.md)   
 [建立模型資料行的別名](../../analysis-services/data-mining/create-an-alias-for-a-model-column.md)  
  
  
