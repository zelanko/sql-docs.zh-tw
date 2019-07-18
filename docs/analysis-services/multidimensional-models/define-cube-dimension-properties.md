---
title: 定義 Cube 維度屬性 |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4401055a15afe73a1f33ee43354f7ee45f887a96
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "68178757"
---
# <a name="define-cube-dimension-properties"></a>定義 Cube 維度屬性
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Cube 維度是 Cube 內之資料庫維度的一個執行個體。 資料庫維度可用於多個 Cube 中，而多個 Cube 維度的基礎是單一資料庫維度。 下表描述 Cube 維度的屬性。  
  
|屬性|描述|  
|--------------|-----------------|  
|**AllMemberAggregationUsage**|控制 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中的彙總設計師所設計之彙總的方式。 此屬性可以有下列的值：<br /><br /> **完整**：每個 cube 的彙總必須包含 「 全部 」 成員。<br /><br /> **無**：Cube 的彙總可以包含的所有成員。 這是預設值。<br /><br /> **不受限制**：彙總設計師沒有任何限制。<br /><br /> **預設值**：不受限制相同的功能。|  
|**描述**|提供層級的描述性名稱。|  
|**DimensionID**|包含資料庫維度的唯一識別碼 (ID)。|  
|**HierarchyUniqueNameStyle**|決定如何為 Cube 維度內所包含的階層產生唯一名稱。 此屬性可以有下列的值：<br /><br /> **IncludeDimensionName**：<br />                    階層之名稱中包含維度的名稱。 這是預設值。<br /><br /> **ExcludeDimensionName**：<br />                    階層之名稱中不包含維度的名稱。|  
|**ID**|包含 Cube 維度的唯一識別碼。|  
|**MemberUniqueNameStyle**|決定如何為 Cube 維度內所包含之階層的成員，產生唯一名稱。 此屬性可以有下列的值：<br /><br /> **Native**：<br />                      [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會自動決定成員的唯一名稱。 這是預設值。<br /><br /> **NamePath**： [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會產生複合名稱，而這個名稱是由成員之每個層級的名稱和標題所組成。|  
|**名稱**|包含 Cube 維度的易記名稱。 依預設，除非已經定義了相同名稱的其他 Cube 維度，否則 Cube 維度的名稱與資料庫維度的名稱相同。|  
|**Visible**|決定 Cube 維度是否可見。 預設值為 **True**。|  
  
## <a name="see-also"></a>另請參閱  
 [維度 &#40;Analysis Services - 多維度資料&#41;](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)  
  
  
