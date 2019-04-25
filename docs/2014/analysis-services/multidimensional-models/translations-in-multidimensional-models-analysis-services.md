---
title: 多維度模型中的翻譯 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensiondesigner.deletelanguagefirm.f1
ms.assetid: 5521f8ef-b10a-4861-9df7-1e43e0a1fb3f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f3238267021c0fd4054fb9757ea8d00cae6114dc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62741146"
---
# <a name="translations-in-multidimensional-models"></a>多維度模型中的翻譯
  多語言支援[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]透過翻譯來完成。 翻譯包含可以使用多種語言呈現之 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件的語言識別碼和屬性繫結。 例如，您可以定義 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫的翻譯，以指定的語言來呈現該資料庫的標題和描述。 如需有關翻譯的詳細資訊，請參閱[Cube 翻譯](../multidimensional-models-olap-logical-cube-objects/cube-translations.md)。  
  
## <a name="defining-translations"></a>定義翻譯  
 您可以在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中定義翻譯，方法是針對要翻譯的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件使用適當的設計師。 定義翻譯會建立 `Translation` 物件，並與適當的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件相關聯，其中會以指定的語言和指定的明確常值，來設定相關聯之 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件的屬性。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中的下列物件和屬性有與其相關聯的翻譯：  
  
|Object|屬性|設計師|  
|------------|----------------|--------------|  
|[資料庫]|`Caption`、 `Description`|[一般&#40;資料庫設計工具&#41; &#40;Analysis Services-多維度資料&#41;](../general-database-designer-analysis-services-multidimensional-data.md)|  
|Cube|`Caption`、 `Description`|[翻譯&#40;Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|量值群組|`Caption`|[翻譯&#40;Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|[量值]|`Caption`、 `DisplayFolder`|[翻譯&#40;Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|Cube 維度|`Caption`|[翻譯&#40;Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|Perspective|`Caption`|[翻譯&#40;Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|關鍵效能指標 (KPI)|`Caption`, `Description`, `DisplayFolder`|[翻譯&#40;Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|動作|`Caption`|[翻譯&#40;Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|命名集|`Caption`|[翻譯&#40;Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|「導出成員」|`Caption`|[翻譯&#40;Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|資料庫維度|`Caption`、 `AttributeAllMember`|[翻譯&#40;維度設計工具&#41; &#40;Analysis Services-多維度資料&#41;](../translations-dimension-designer-analysis-services-multidimensional-data.md)|  
|屬性|`Caption`, `CaptionColumn`<sup>1</sup>, `AttributeHierarchyDisplayFolder`, `NamingTemplate`, `MembersWithDataCaption`|[翻譯&#40;維度設計工具&#41; &#40;Analysis Services-多維度資料&#41;](../translations-dimension-designer-analysis-services-multidimensional-data.md)|  
|階層|`Caption`、 `AllMemberName`|[翻譯&#40;維度設計工具&#41; &#40;Analysis Services-多維度資料&#41;](../translations-dimension-designer-analysis-services-multidimensional-data.md)|  
|層級|`Caption`|[翻譯&#40;維度設計工具&#41; &#40;Analysis Services-多維度資料&#41;](../translations-dimension-designer-analysis-services-multidimensional-data.md)|  
  
 <sup>1</sup> `CaptionColumn`屬性的屬性可以繫結至資料來源檢視中的資料行，而且可以使用指定的執行個體，與其他翻譯不同的 Windows 定序。  
  
### <a name="defining-attribute-translations"></a>定義屬性翻譯  
 與資料庫維度中之屬性相關聯的翻譯和其他翻譯在處理方式上有下列不同：  
  
-   並非明確常值，而是資料行繫結可與 `CaptionColumn` 屬性 (Property) 相關聯，以便該屬性 (Attribute) 之成員的成員名稱可以翻譯。  
  
-   為該執行個體指定可使用之定序以外的 Windows 定序，以便針對翻譯中指定的語言適當地排序該屬性中的成員。  
  
 您可以使用**屬性資料翻譯** 對話方塊中的[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]資料庫維度中定義屬性的翻譯。 如需詳細資訊**屬性資料翻譯** 對話方塊中，請參閱[屬性資料翻譯對話方塊&#40;Analysis Services-多維度資料&#41;](../attribute-data-translation-dialog-box-analysis-services-multidimensional-data.md)。  
  
## <a name="resolving-translations"></a>解析翻譯  
 如果用戶端應用程式要求指定之語言識別碼中的資訊， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體會嘗試將 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件的資料和中繼資料解析成最接近的語言識別碼。 如果用戶端應用程式未指定預設語言，或指定中性地區設定識別碼 (0) 或處理序預設語言識別碼 (1024)，則 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會使用執行個體的預設語言來傳回 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件的資料和中繼資料。  
  
 如果用戶端應用程式指定的語言識別碼不是預設語言識別碼，則執行個體會對所有可用的物件逐一查看所有可用的翻譯。 如果指定的語言識別碼符合翻譯的語言識別碼， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 就會傳回該翻譯。 如果找不到相符項目， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會嘗試使用下列其中一個方法，來傳回具有最接近指定之語言識別碼的翻譯：  
  
-   針對下列語言識別碼，如果尚未定義指定之語言識別碼的翻譯，則 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會嘗試使用替代語言識別碼：  
  
    |指定的語言識別碼|替代語言識別碼|  
    |-----------------------------------|-----------------------------------|  
    |3076 - 中文 (中國香港特別行政區)|1028 - 中文 (台灣)|  
    |5124 - 中文 (澳門特別行政區)|1028 - 中文 (台灣)|  
    |1028 - 中文 (台灣)|預設語言|  
    |4100 - 中文 (新加坡)|2052 - 中文 (中華人民共和國)|  
    |2074 - 克羅埃西亞文|預設語言|  
    |3098 - 克羅埃西亞文 (斯拉夫文)|預設語言|  
  
-   針對所有其他指定的語言識別碼， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會擷取 (extract) 所指定之語言識別碼的主要語言，並擷取 (retrieve) Windows 所指出的語言識別碼作為主要語言的最符合項目。 如果找不到最符合之語言識別碼的翻譯，或指定的語言識別碼是主要語言的最符合項目，則使用預設語言。  
  
## <a name="deleting-translation-objects"></a>刪除翻譯物件  
 您可以用滑鼠右鍵按一下維度或 Cube 設計師中的翻譯物件，永久將它移除。 由於您無法還原或回收刪除的物件，因此務必要在繼續進行之前檢閱受影響物件的清單。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 多維度的全球化案例](../globalization-scenarios-for-analysis-services-multiidimensional.md)   
 [語言和定序 &#40;Analysis Services&#41;](../languages-and-collations-analysis-services.md)  
  
  
