---
title: 選取維度屬性 （維度精靈） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensionwizard.dimensionattributes.f1
ms.assetid: f58a3e14-ab27-44d3-8c26-f5c9ee7583b0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7abb4560696dba21512066a7ff0ba3153ae2319a
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52508006"
---
# <a name="select-dimension-attributes-dimension-wizard"></a>選取維度屬性 (維度精靈)
  使用 **[選取維度屬性]** 頁面，即可選取和修改要建立之維度的屬性。  
  
> [!NOTE]  
>  如果您無法讀取任何資料行的值，請將精靈視窗最大化，然後變更每個資料行標題的寬度，直到可以讀取這些值為止。  
  
 **若要開啟 維度精靈**  
  
-   在方案總管的 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中，以滑鼠右鍵按一下 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 專案的 [維度] 資料夾，然後按一下 [新增維度]。  
  
## <a name="options"></a>選項。  
 (具有核取方塊的資料行)  
 選取即可將屬性包含在維度中。  
  
 若要包含特定屬性，請選取該屬性的核取方塊。  
  
 若要包含所有屬性，請選取資料行標頭中的核取方塊。  
  
> [!NOTE]  
>  您無法清除索引鍵屬性的核取方塊。  
  
 **屬性名稱**  
 列出可用的屬性。  
  
 若要變更屬性的名稱，請按一下屬性名稱，然後輸入屬性的新名稱。  
  
 **啟用瀏覽**  
 選取即可讓屬性供使用者用來瀏覽和篩選。 您必須針對索引鍵屬性選取 **[啟用瀏覽]** 。 若為非索引鍵屬性 (Attribute)，預設值是不選取 [啟用瀏覽]，因而導致非索引鍵屬性 (Attribute) 只能顯示為成員屬性 (Property)。  
  
 在大部分情況下，您可以透過分別將 `AttributeHierarchyEnabled` 屬性 (Property) 設定為 `True` 或 `False`，讓屬性 (Attribute) 可以或無法用於瀏覽。 不過，在下列三個情況中，精靈會使用不同的設定。  
  
|案例|[設定]|  
|----------|--------------|  
|維度包含父子式階層而且沒有選取 [啟用瀏覽]|精靈會維持 `AttributeHierarchyEnabled` 屬性 (Property) 設定為 `True`，並將索引鍵屬性 (Attribute) 的 `AttributeHierarchyVisible` 屬性 (Attribute) 設定為 `False`。|  
|維度中的資料表包含指向不在維度中之資料表的外部索引鍵|雖然精靈會選取外部索引鍵當做要包含的屬性，但是不會選取 **[啟用瀏覽]**。 如果您保留這些設定，屬性 (Attribute) 的 `AttributeHiearchyEnabled` 屬性 (Property) 將設定為 `True`，而且 `AttributeHieararchyVisible` 屬性 (Property) 將設定為 `False`。|  
|維度包含透過可為 Null 之外部索引鍵資料行存取的雪花資料表<br /><br /> -和-<br /><br /> 沒有針對以雪花資料表之索引鍵為基礎的屬性選取 [啟用瀏覽]|精靈將會建立新的屬性 (Attribute)，其中 `AttributeHiearchyEnabled` 屬性 (Property) 設定為 `True`，而且 `AttributeHieararchyVisible` 屬性 (Property) 設定為 `False`。|  
  
 **屬性類型**  
 (選擇性) 設定屬性的類型。 預設值是 **[一般]**。 屬性類型會將屬性可能包含之資訊的相關指引提供給用戶端應用程式。  
  
## <a name="see-also"></a>另請參閱  
 [維度精靈 F1 說明](dimension-wizard-f1-help.md)   
 [維度&#40;Analysis Services-多維度資料&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)   
 [多維度模型中的維度](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
