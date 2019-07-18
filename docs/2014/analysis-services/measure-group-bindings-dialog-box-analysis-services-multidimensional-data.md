---
title: 量值群組繫結對話方塊 (Analysis Services-多維度資料) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.dimensionusage.definerelationship.measuregroupbindings.f1
helpviewer_keywords:
- Measure Group Bindings dialog box
ms.assetid: ed642780-5350-438e-af73-b9ceab3f876d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4d3d04692ac6576e76d2b630fb5cacb4f57db959
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66077861"
---
# <a name="measure-group-bindings-dialog-box-analysis-services---multidimensional-data"></a>量值群組繫結對話方塊 (Analysis Services - 多維度資料)
  使用 [量值群組繫結]  對話方塊，即可針對一般維度關聯性，建立及修改 Cube 維度中之非資料粒度屬性，與量值群組中之資料行之間的直接關聯性；以及從 [定義關聯性]  對話方塊中，指定 Cube 維度中之任何屬性的 Null 處理選項。  
  
## <a name="options"></a>選項  
 **量值群組資料表**  
 顯示所選取量值群組之事實資料表的名稱。  
  
 **屬性**  
 顯示屬性和維度資料表組成的方格。 選取屬性 (Attribute)，即可針對所選取的屬性 (Attribute) 建立或修改 **[關聯性]** 中的屬性 (Property)。 方格包含下列資料行：  
  
|選項|定義|  
|------------|----------------|  
|**屬性名稱**|顯示屬性的名稱。|  
|**維度資料表**|顯示作為屬性基礎之維度資料表的名稱。|  
  
 **關聯性**  
 顯示由選取之屬性的維度資料表資料行，與選取之量值群組的事實資料表資料行之間的關聯性所組成的方格，以及關聯性的 Null 處理選項。 方格包含下列資料行：  
  
|選項|定義|  
|------------|----------------|  
|**維度資料行**|顯示來自維度資料表中，作為 **[屬性]** 中所選取屬性之基礎的資料行。|  
|**量值群組資料行**|選取 **[繼承自維度]** 即可使用繼承自維度的量值群組關聯性；或者從作為量值群組之基礎的事實資料表中選取資料行，即可明確地定義關聯性。|  
|**Null 處理**|為屬性選取 Null 處理選項。 如需 Null 處理選項的詳細資訊，請參閱 [NullProcessing 元素 &#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/properties/nullprocessing-element-assl)。|  
  
## <a name="see-also"></a>另請參閱  
 [定義關聯性對話方塊&#40;Analysis Services-多維度資料&#41;](define-relationship-dialog-box-analysis-services-multidimensional-data.md)   
 [Analysis Services Designers and Dialog Boxes&#40;多維度資料&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)  
  
  
