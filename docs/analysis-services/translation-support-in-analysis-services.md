---
title: "Analysis Services 中的翻譯支援 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Business Intelligence Development Studio, translations [Analysis Services]
- translations [Analysis Services], about translations
- object translations [Analysis Services]
- language identifiers [Analysis Services]
- attribute translations [Analysis Services]
- translations [Analysis Services]
ms.assetid: 018471e0-3c82-49ec-aa16-467fb58a6d5f
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: fc97336300fef2dd621f1f151ff39a04cc3fbfe6
ms.sourcegitcommit: 82c9868b5bf95e5b0c68137ba434ddd37fc61072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/22/2018
---
# <a name="translation-support-in-analysis-services"></a>Analysis Services 中的翻譯支援
[!INCLUDE[ssas-appliesto-sqlas-aas](../includes/ssas-appliesto-sqlas-aas.md)]

  在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料模型中，您可以內嵌標題或描述的多個翻譯，根據 LCID 提供文化特性的字串。 若為多維度模型，您可以為資料庫名稱、Cube 物件和資料庫維度物件加入翻譯。 若為表格式模型，您可以翻譯資料表和資料行的標題和描述。  
  
 定義翻譯會在模型內建立中繼資料和翻譯的標題，但若要在用戶端應用程式中轉譯當地語系化的字串，您必須在物件上設定 **Language** 屬性，或在連接字串上傳遞 **Culture** 或 **Locale Identifier** 參數 (例如，藉由設定 `LocaleIdentifier=1036` 以傳回法文字串)。  
  
 如果您想要支援相同物件之多個不同語言且同時的翻譯，請規劃使用 **Locale Identifier** 。 設定 **Language** 屬性雖然有效，但也會影響處理和查詢，而可能會有非預期的結果。 設定 **Locale Identifier** 是較佳的選擇，因為它只會用來傳回翻譯的字串。  
  
 翻譯是由地區設定識別碼 (LCID)、物件的翻譯標題 (例如維度或屬性名稱)，以及 (選擇性) 以目標語言提供資料值的資料行繫結所組成。 您可以有多個翻譯，但任何一個指定的連接只能使用一個翻譯。 理論上，您可以內嵌在模型中的翻譯數目沒有限制，但每個翻譯都會增加測試的複雜性，且所有翻譯都必須共用相同的定序，因此當您設計方案時，請記住這些原本就有的條件約束。  
  
> [!TIP]  
>  您可以使用用戶端應用程式 (例如 Excel、Management Studio 和 SQL Server Profiler) 來傳回翻譯的字串。 如需詳細資訊，請參閱 [全球化秘訣和最佳做法 &#40;Analysis Services&#41;](../analysis-services/globalization-tips-and-best-practices-analysis-services.md) (全球化秘訣和最佳做法 (Analysis Services))。  
  
## <a name="how-to-add-translated-metadata-to-model-in-analysis-services"></a>如何將翻譯的中繼資料加入 Analysis Services 模型中  
 請前往下列連結取得逐步指示：  
  
-   [表格式模型 &#40;Analysis Services&#41; 中的翻譯](../analysis-services/tabular-models/translations-in-tabular-models-analysis-services.md)  
  
-   [多維度模型中的翻譯 &#40;Analysis Services&#41;](../analysis-services/multidimensional-models/translations-in-multidimensional-models-analysis-services.md)  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 的全球化案例](../analysis-services/globalization-scenarios-for-analysis-services.md)   
 [語言和定序 &#40;Analysis Services &#41;](../analysis-services/languages-and-collations-analysis-services.md)   
 [設定或變更資料行定序](../relational-databases/collations/set-or-change-the-column-collation.md)   
 [全球化秘訣和最佳作法 &#40;Analysis Services &#41;](../analysis-services/globalization-tips-and-best-practices-analysis-services.md)  
  
  
