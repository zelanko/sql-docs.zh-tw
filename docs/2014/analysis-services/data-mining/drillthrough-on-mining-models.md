---
title: 採礦模型的鑽研 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: f179a467-7d03-4d61-8e9a-6b5afb5fc2d5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b955ade0251f43d6a482abe346c286c6bafd0ce7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66084600"
---
# <a name="drillthrough-on-mining-models"></a>採礦模型的鑽研
  「鑽研」  表示查詢採礦模型或採礦結構並取得模型中未公開之詳細資料的能力。  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 提供了兩種不同的鑽研選項來鑽研案例資料。 您可以鑽研用來建立資料的案例，也可以鑽研採礦結構中的案例。  
  
## <a name="drillthrough-to-model-cases-vs-drillthrough-to-structure"></a>鑽研模型案例和鑽研結構的比較  
 鑽研 **模型案例** 對於尋找模型中規則、模式或叢集的詳細資料很有幫助。 例如，您不會使用客戶連絡資訊用於群集模型中的分析，即使資料是使用鑽研，您可以存取該資訊從模型。  
  
 反之， **鑽研結構** 資料用意在於提供對模型中無法使用之資訊的存取。 例如，一些結構資料行可能因為資料類型不相容或者資料未用於分析而從模型中排除。  
  
## <a name="enabling-drillthrough-on-a-model"></a>啟用模型鑽研  
 若要對採礦模型使用鑽研，必須符合下列條件：  
  
-   只在模型案例上設定鑽研是可行的，但是不能在採礦結構上設定，但並不是反之亦然。  換句話說，必須在採礦模型上啟用鑽研，以允許鑽研至採礦結構。  
  
-   根據預設，模型和結構上的鑽研都會停用。 如果您使用資料採礦精靈，啟用鑽研模型案例的選項位於精靈的最後一頁。  
  
-   您可以在現有的採礦模型上加入鑽研的能力，但是如果您這樣做，就必須先重新處理模型，然後才能鑽研資料。  
  
-   除非已經保留定型程序期間建立的快取，否則鑽研無法運作。 如需控制快取之屬性的詳細資訊，請參閱 [採礦結構的鑽研](drillthrough-on-mining-structures.md)。  
  
## <a name="models-that-support-drillthrough"></a>支援鑽研的模型  
 如果採礦模型已經設定成允許鑽研，而且您擁有適當的權限，當您瀏覽此模型時，可以在適當的檢視器中按一下節點，然後擷取有關該特定節點中案例的詳細資訊。  
  
 並非所有模型都支援鑽研，這取決於建立模型所使用的演算法。 下表列出不支援鑽研或是在限制之下支援鑽研的模型類型。 如果模型類型未列在這裡，就會支援鑽研。  
  
|**演算法名稱**|**支援鑽研**|  
|------------------------|----------------------------------|  
|Microsoft 貝氏機率分類演算法|不支援。<br /><br /> 這些演算法不會將案例指派給內容中的特定節點。|  
|Microsoft 類神經網路演算法|不支援。<br /><br /> 這些演算法不會將案例指派給內容中的特定節點。|  
|Microsoft 羅吉斯迴歸演算法|不支援。<br /><br /> 這些演算法不會將案例指派給內容中的特定節點。|  
|Microsoft 線性迴歸演算法|支援。<br /><br /> 不過，由於此模型會建立單一節點 `All`，因此鑽研會傳回模型的所有定型案例。 如果定型集很龐大，載入結果的時間可能會很長。|  
|Microsoft 時間序列演算法|支援。<br /><br /> 不過，您無法使用資料採礦設計師中的 **[採礦模型檢視器]** ，鑽研結構或案例資料。 您必須改為建立 DMX 查詢。<br /><br /> 此外，您無法鑽研至特定節點，或撰寫 DMX 查詢來擷取時間序列模型之特定節點中的案例。 您可以使用其他準則 (例如日期或屬性值)，從模型或結構內部擷取案例資料。<br /><br /> 如果您想要檢視 Microsoft 時間序列演算法所建立之 ARTXP 和 ARIMA 節點的詳細資訊，使用 [Microsoft 一般內容樹狀檢視器 &#40;資料採礦&#41;](../microsoft-generic-content-tree-viewer-data-mining.md) 可能更容易。|  
  
## <a name="related-tasks"></a>相關工作  
 如需有關如何將鑽研用於採礦模型的詳細資訊，請參閱下列主題。  
  
|工作|連結|  
|-----------|-----------|  
|在採礦模型檢視器中使用鑽研|[從模型檢視器使用鑽研](use-drillthrough-from-the-model-viewers.md)|  
|使用鑽研擷取模型的案例資料|[鑽研採礦模型的案例資料](drill-through-to-case-data-from-a-mining-model.md)|  
|針對現有的採礦模型啟用鑽研|[針對採礦模型啟用鑽研](enable-drillthrough-for-a-mining-model.md)|  
|參閱特定模型類型的鑽研查詢範例。|[資料採礦查詢](data-mining-queries.md)|  
|在採礦模型精靈中啟用鑽研|[正在完成精靈 &#40;資料採礦精靈&#41;](../completing-the-wizard-data-mining-wizard.md)。|  
  
## <a name="see-also"></a>另請參閱  
 [採礦結構的鑽研](drillthrough-on-mining-structures.md)  
  
  
