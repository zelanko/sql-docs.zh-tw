---
title: 資料來源檢視 (Analysis Services) 中定義邏輯主索引鍵 |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 418d671fb269a8b70fca19b2900a9958db96800d
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="define-logical-primary-keys-in-a-data-source-view-analysis-services"></a>在資料來源檢視中定義邏輯主索引鍵 (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [資料來源檢視精靈] 和資料來源檢視設計師會自動根據基礎資料庫資料表，針對加入到資料來源檢視中的資料表定義主索引鍵。  
  
 您有時候可能需要手動定義資料來源檢視中的主索引鍵。 例如，基於效能或設計考量，資料來源中的資料表可能並未明確定義主索引鍵資料行。 具名查詢和檢視也可能會省略資料表的主索引鍵資料行。 如果資料表、檢視或具名查詢沒有定義實體主索引鍵，您可以在資料來源檢視設計師中，以手動方式在資料表、檢視或具名查詢中定義邏輯主索引鍵。  
  
## <a name="set-a-logical-primary-key"></a>設定邏輯主索引鍵  
 在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中必須有主索引鍵，以唯一識別資料表中的記錄、識別維度資料表中的索引鍵資料行，並支援資料表、檢視及具名查詢之間的關聯性。 這些關聯性是用來建構一些查詢，以便擷取基礎資料來源中的資料和中繼資料，以及利用進階商業智慧的功能。  
  
 任何資料行皆可用於邏輯主索引鍵，包括具名計算。 當您建立邏輯主索引鍵時，唯一條件約束會建立在資料來源檢視中，並標示為主索引鍵條件約束。 在選取之資料表中指定的任何其他現有的邏輯主索引鍵會遭到刪除。  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟含有您想在其中設定邏輯主索引鍵之資料來源檢視的專案，或連接到包含此資料來源檢視的資料庫。  
  
2.  在方案總管中，展開 [資料來源檢視] 資料夾，然後按兩下資料來源檢視。  
  
     若要尋找資料表或檢視表，您可以按一下 [資料來源檢視] 功能表，或是以滑鼠右鍵按一下 [資料表] 或 [圖表] 窗格的開放區域，即可使用 [尋找資料表] 選項。  
  
3.  在 [資料表] 或 [圖表] 窗格中，以滑鼠右鍵按一下您要用來定義邏輯主索引鍵的一或多個資料行，然後按一下 [設定邏輯主索引鍵]。  
  
     設定邏輯主索引鍵的選項只提供給沒有主索引鍵的資料表使用。  
  
     請注意，在您設定主索引鍵後，索引鍵圖示即會識別主索引鍵資料行。  
  
## <a name="see-also"></a>另請參閱  
 [多維度模型中的資料來源檢視](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)   
 [在資料來源檢視 & #40; 中定義具名的計算Analysis Services & #41;](../../analysis-services/multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)  
  
  
