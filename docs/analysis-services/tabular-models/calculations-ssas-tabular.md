---
title: "計算 (SSAS 表格式) |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 738816e3-0e1d-44a5-8d1b-81068dce8ac0
caps.latest.revision: "19"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9f2d85a5064b41a5cae0fd63cda735ea6edcd3a2
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="calculations-ssas-tabular"></a>計算 (SSAS 表格式)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]您匯入資料到模型之後，您可以新增計算，以彙總、 篩選、 擴充、 結合及保護資料。 表格式模型使用 Data Analysis Expression (DAX) 這個新的公式語言以建立自訂計算。 在表格式模型中，您使用 DAX 公式建立的計算會用於 *「導出資料行」*(Calculated Column)、 *「量值」*(Measures) 和 *「資料列篩選」*(Row Filters)。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|描述|  
|-----------|-----------------|  
|[了解表格式模型中的 DAX &#40;SSAS 表格式&#41;](../../analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular.md)|描述 Data Analysis Expressions (DAX) 公式語言，可用來在表格式模型中建立導出資料行、量值和資料列篩選的計算。|  
|[DirectQuery 模式中的 DAX 公式相容性 (SQL Server Analysis Services)](http://msdn.microsoft.com/en-us/981b6a68-434d-4db6-964e-d92f8eb3ee3e)|描述差異、列出 DirectQuery 模式不支援的函數，並且列出受支援但可能會傳回不同結果的函數。|  
|[Data Analysis Expressions (DAX) 參考](http://msdn.microsoft.com/en-us/70a82136-0926-4a91-bcb3-e18e82593b0d)|本節提供 DAX 語法、運算子和函數的詳細描述。|  
  
> [!NOTE]  
>  本節中不提供建立計算的逐步工作。 由於計算是在導出資料行、量值和資料列篩選 (依角色) 中指定，因此在與這些功能相關的工作中，會提供建立 DAX 公式的指示。 如需詳細資訊，請參閱[建立導出資料行 &#40;SSAS 表格式&#41;](../../analysis-services/tabular-models/ssas-calculated-columns-create-a-calculated-column.md)、[建立及管理量值 &#40;SSAS 表格式&#41;](../../analysis-services/tabular-models/create-and-manage-measures-ssas-tabular.md) 和[建立及管理角色 &#40;SSAS 表格式&#41;](../../analysis-services/tabular-models/create-and-manage-roles-ssas-tabular.md)。  
  
> [!NOTE]  
>  DAX 也可以用來查詢表格式模型，因此，本節中的主題將特別著重在使用 DAX 公式建立計算。  
  
  
