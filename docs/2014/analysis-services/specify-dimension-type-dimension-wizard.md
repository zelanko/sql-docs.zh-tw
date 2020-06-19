---
title: 指定維度類型（維度 Wizard） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensionwizard.bidimensionproperties.f1
ms.assetid: 3215282a-532d-4ff2-b721-286f088967fc
author: minewiskan
ms.author: owend
ms.openlocfilehash: 0a280411bc05bdab416a177cea89f252a53ac0fc
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84940399"
---
# <a name="specify-dimension-type-dimension-wizard"></a>指定維度類型 (維度精靈)
  使用 **[指定維度類型]** 頁面來定義維度類型，並將與所選取之維度類型相關聯的特殊屬性類型加入至維度。  
  
> [!NOTE]  
>  只有當您在 [選取維度類型]**** 頁面上選取 [標準維度]**** 時，才會顯示此頁面。  
  
## <a name="options"></a>選項。  
 **維度類型**  
 選取維度的維度類型。 下表列出可用的維度類型。  
  
|值|描述|  
|-----------|-----------------|  
|**帳戶**|帳戶維度包含資料和代表帳戶清單的中繼資料。<br /><br /> 如需帳戶維度的詳細資訊，請參閱 [建立父子式類型維度的財務帳戶](multidimensional-models/database-dimensions-finance-account-of-parent-child-type.md)。|  
|**BillOfMaterials**|用料表 (或 BOM) 維度是一般維度，其中的資料和中繼資料代表存貨或製造資訊，例如產品的零件清單。<br /><br /> 如需一般維度的詳細資訊，請參閱 [維度類型](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)。|  
|**通道**|通道維度是一般維度，其中的資料和中繼資料代表通道資訊。<br /><br /> 如需一般維度的詳細資訊，請參閱 [維度類型](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)。|  
|**貨幣**|貨幣維度包含代表貨幣資訊的資料和中繼資料。<br /><br /> 如需貨幣維度的詳細資訊，請參閱 [建立貨幣類型維度](multidimensional-models/database-dimensions-create-a-currency-type-dimension.md)。|  
|**客戶**|客戶維度是一般維度，其中的資料和中繼資料代表客戶或連絡資訊。<br /><br /> 如需一般維度的詳細資訊，請參閱 [維度類型](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)。|  
|**地理位置**|地理位置維度是一般維度，其中的資料和中繼資料代表地理資訊，例如城市或郵遞區號。<br /><br /> 如需一般維度的詳細資訊，請參閱 [維度類型](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)。|  
|**組織**|組織維度是一般維度，其中的資料和中繼資料代表組織的資訊，例如員工或分公司。<br /><br /> 如需一般維度的詳細資訊，請參閱 [維度類型](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)。|  
|**產品**|產品維度是一般維度，其中的資料和中繼資料代表產品資訊。<br /><br /> 如需一般維度的詳細資訊，請參閱 [維度類型](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)。|  
|**促銷**|促銷維度是一般維度，其中的資料和中繼資料代表行銷促銷資訊。<br /><br /> 如需一般維度的詳細資訊，請參閱 [維度類型](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)。|  
|**數量**|數量的維度是一般維度，其中的資料和中繼資料代表數量的資訊。<br /><br /> 如需一般維度的詳細資訊，請參閱 [維度類型](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)。|  
|**匯率**|匯率維度包含代表匯率和貨幣轉換資訊的資料和中繼資料。|  
|**標準**|一般維度是中最常使用的維度類型 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 。<br /><br /> 如需一般維度的詳細資訊，請參閱 [維度類型](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)。|  
|**案例**|狀況維度是一般維度，其中的資料和中繼資料代表計畫或策略分析資訊。<br /><br /> 如需一般維度的詳細資訊，請參閱 [維度類型](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)。|  
|**Time**|時間維度包含時間導向的資料和中繼資料。<br /><br /> 如需時間維度的詳細資訊，請參閱 [建立日期類型維度](multidimensional-models/database-dimensions-create-a-date-type-dimension.md)。|  
|**公用程式**|通用維度是一般維度，其中的資料和中繼資料代表無法符合另一個維度類型的資訊。<br /><br /> 如需一般維度的詳細資訊，請參閱 [維度類型](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)。|  
  
## <a name="dimension-attributes-options"></a>維度屬性選項  
  
> [!NOTE]  
>  只有當選取的 **[維度類型]** 有與其相關聯的特殊屬性類型時，才可以使用此章節中的選項。 並非所有的維度類型都有與其相關聯的特殊屬性類型。  
  
 **涉及**  
 選取即可將屬性類型包含在維度中。  
  
 **屬性類型**  
 顯示與 [維度類型]**** 中所選取之維度類型相關聯的屬性類型。 如需屬性類型的詳細資訊，請參閱 [Type 元素 &#40;DimensionAttribute&#41; &#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/properties/type-element-dimensionattribute-assl)。  
  
 **維度屬性**  
 選取維度屬性，維度精靈會將顯示在 [屬性類型]**** 中的特殊屬性類型指派給該維度屬性。  
  
## <a name="see-also"></a>另請參閱  
 [維度嚮導 F1 說明](dimension-wizard-f1-help.md)   
 [維度 &#40;Analysis Services 多維資料&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)   
 [多維度模型中的維度](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
