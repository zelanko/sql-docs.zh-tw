---
title: Analysis Services 表格式模型中的計算 |Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c7096cac1f4721531f1905b11f2ca3b901661204
ms.sourcegitcommit: a6949111461eda0cc9a71689f86b517de3c5d4c1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2019
ms.locfileid: "67263434"
---
# <a name="calculations-in-tabular-models"></a>表格式模型中的計算
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  將資料匯入到模型之後，您可以新增計算以彙總、篩選、擴充、結合資料，以及保護資料安全。 表格式模型使用 Data Analysis Expression (DAX) 這個新的公式語言以建立自訂計算。 在表格式模型中，您使用 DAX 公式建立的計算會用於 *「導出資料行」* (Calculated Column)、 *「量值」* (Measures) 和 *「資料列篩選」* (Row Filters)。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|描述|  
|-----------|-----------------|  
|[了解表格式模型中的 DAX](../../analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular.md)|描述 Data Analysis Expressions (DAX) 公式語言，可用來在表格式模型中建立導出資料行、量值和資料列篩選的計算。|  
|[在 DirectQuery 模式中的 DAX 公式相容性](http://msdn.microsoft.com/981b6a68-434d-4db6-964e-d92f8eb3ee3e)|描述差異、列出 DirectQuery 模式不支援的函數，並且列出受支援但可能會傳回不同結果的函數。|  
|[Data Analysis Expressions (DAX) 參考](/dax/data-analysis-expressions-dax-reference)|本節提供 DAX 語法、運算子和函數的詳細描述。|  
  
> [!NOTE]  
>  本節中不提供建立計算的逐步工作。 由於計算是在導出資料行、量值和資料列篩選 (依角色) 中指定，因此在與這些功能相關的工作中，會提供建立 DAX 公式的指示。 如需詳細資訊，請參閱 <<c0> [ 建立 「 計算結果欄](../../analysis-services/tabular-models/ssas-calculated-columns-create-a-calculated-column.md)，[建立及管理量值](../../analysis-services/tabular-models/create-and-manage-measures-ssas-tabular.md)，並[建立及管理角色](../../analysis-services/tabular-models/create-and-manage-roles-ssas-tabular.md)。  
  
> [!NOTE]  
>  DAX 也可以用來查詢表格式模型，因此，本節中的主題將特別著重在使用 DAX 公式建立計算。  
  
  
