---
title: 對採礦結構的鑽取 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a0b00a3b-f9db-4289-a8cb-ddf600cd64ac
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 71212f81a2f42fbbff28e04b4632bc2120362089
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66084576"
---
# <a name="drillthrough-on-mining-structures"></a>採礦結構的鑽研
  「*鑽取*」是指查詢「採礦模型」或「採礦結構」，並取得不在模型中公開之詳細資料的能力。  
  
 
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 提供了兩種不同的鑽研選項來鑽研案例資料。 您可以鑽研用來建立採礦模型的資料，也可以鑽研採礦結構中的來源資料。  
  
## <a name="drillthrough-to-model-cases-vs-drillthrough-to-structure"></a>鑽研模型案例和鑽研結構的比較  
 鑽研 **模型案例** 對於尋找模型中規則、模式或叢集的詳細資料很有幫助。  
  
 反之， **鑽研結構** 資料用意在於提供對模型中無法使用之資訊的存取。 例如，如果您具有適當的權限，可能要確定哪些資料列用於模型定型，哪些資料列用於測試。  
  
 還可以檢視分析中未使用之資料的屬性，只要這些屬性已包含在結構定義中。 例如，採礦結構通常支援許多不同類型的模型，並且一些結構資料行可能因為資料類型不相容或者資料未用於分析而從模型中排除。 例如，您不會在叢集模型中使用客戶連絡資訊，即使資料已包含在結構中，但透過啟用鑽研，不需要對資料來源執行單獨查詢即可取得對此資訊的存取。  
  
## <a name="enabling-drillthrough-to-structure-data"></a>啟用結構資料鑽研  
 若要對採礦結構使用鑽研，必須符合下列條件：  
  
-   還必須在模型上啟用鑽研。 根據預設，這兩種類型的鑽研都已停用。 若要在資料採礦精靈中啟用鑽研，請選取位於精靈最後一頁啟用鑽研模型案例的選項。 您也可以稍後變更 `AllowDrillthrough` 屬性，在模型上新增鑽研的能力。  
  
-   如果您使用 DMX 來建立採礦結構，請使用 WITH DRILLTHROUGH 子句。 如需詳細資訊，請參閱 [CREATE MINING STRUCTURE &#40;DMX&#41;](/sql/dmx/create-mining-structure-dmx)。  
  
-   鑽研藉由擷取處理採礦結構時快取之定型案例的相關資訊來運作。 因此，如果您將 <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> 屬性變更為 `ClearAfterProcessing`，在處理結構之後清除快取的資料，鑽研將不會運作。 若要啟用結構資料行的鑽研功能，您必須將 <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> 屬性變更為 `KeepTrainingCases`，然後重新處理結構。  
  
-   確認這兩個[AllowDrillThrough](https://docs.microsoft.com/bi-reference/assl/properties/allowdrillthrough-element-assl)屬性都設定為`True`。 此外，您必須是針對結構和模型同時擁有鑽研權限之角色的成員。  
  
## <a name="security-issues-for-drillthrough"></a>鑽研的安全性問題  
 鑽研權限是在結構和模型上分別設定的。 即使您沒有結構的權限，模型權限還是可以讓您從模型進行鑽研。 結構的鑽研權限可以使用 [StructureColumn &#40;DMX&#41;](/sql/dmx/structurecolumn-dmx) 函數，提供將結構資料行從模型加入到鑽研查詢的額外功能。  
  
 如需如何在 Analysis Services 中建立角色和指派權限的資訊，請參閱[角色設計師 &#40;Analysis Services - 多維度資料&#41;](https://msdn.microsoft.com/library/ms189696(v=sql.120).aspx)。  
  
> [!NOTE]  
>  如果您在採礦結構和採礦模型上都啟用鑽研，則任何使用者 (針對採礦模型具有鑽研權限之角色的成員) 也可以檢視採礦結構中的資料行，即使這些資料行未包含在採礦模型中也一樣。 因此，若要保護機密資料，您應該設定資料來源檢視來遮罩個人資訊，並只有在必要時才允許採礦結構的鑽研存取。  
  
## <a name="related-tasks"></a>相關工作  
 如需有關如何將鑽研用於採礦模型的詳細資訊，請參閱下列主題。  
  
|||  
|-|-|  
|從採礦模型檢視器對結構使用鑽研|[從模型檢視器使用鑽研](use-drillthrough-from-the-model-viewers.md)|  
|參閱特定模型類型的鑽研查詢範例。|[資料採礦查詢](data-mining-queries.md)|  
|取得有關適用於特定採礦結構和採礦模型之權限的詳細資訊。|[授與資料採礦結構和模型的許可權 &#40;Analysis Services&#41;](../multidimensional-models/grant-permissions-on-data-mining-structures-and-models-analysis-services.md)|  
  
## <a name="see-also"></a>另請參閱  
 [採礦模型的鑽研](drillthrough-on-mining-models.md)  
  
  
