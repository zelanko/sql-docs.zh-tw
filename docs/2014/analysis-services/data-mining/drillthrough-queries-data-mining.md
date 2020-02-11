---
title: 鑽取查詢（資料採礦） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- AllowDrillThrough property
- drillthrough [Analysis Services]
- drillthrough [DMX]
ms.assetid: 246c784b-1b0c-4f0b-96f7-3af265e67051
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ca74fe9ec36262130e01a58280f9d966c35c3485
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66084544"
---
# <a name="drillthrough-queries-data-mining"></a>鑽研查詢 (資料採礦)
  
  *「鑽研查詢」* (Drillthrough query) 可讓您傳送查詢至採礦模型，以擷取基礎案例或結構的詳細資料。 如果您想要檢視用來定型模型的案例與用來測試模型的案例，或者您想要查看案例資料的其他詳細資料，鑽研就很有用。  
  
 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料採礦提供了兩種不同的鑽研選項：  
  
-   鑽研到 **模型案例**  
  
     當您想要從模型中的特定模式（例如，決策樹的叢集或分支）移至模型案例時，會使用 [鑽取]，並查看有關個別案例的詳細資料。  
  
-   鑽研到 **結構案例**  
  
     當結構包含可能無法用於模型的資訊時，就適合鑽研到結構案例。 例如，您不會將客戶連絡資訊用於叢集模型中，即使資料包含在結構中也一樣。 不過，在您建立模型之後，可能會想要擷取分組成特定叢集之客戶的連絡資訊。  
  
 本章節提供如何建立這些查詢的範例。  
  
 [在資料採礦設計工具中使用鑽取](#bkmk_Designer)  
  
 [使用 DMX 建立鑽取查詢](#bkmk_DMX)  
  
 [使用鑽取時的考慮](#bkmk_Considerations)  
  
-   [安全性問題](#bkmk_Security)  
  
-   [限制](#bkmk_Limits)  
  
##  <a name="bkmk_Designer"></a>在資料採礦設計工具中使用鑽取  
 如果採礦模型已經設定成允許鑽研，而且您擁有適當的權限，當您瀏覽此模型時，可以在適當的檢視器中按一下節點，然後擷取有關該特定節點中案例的詳細資訊。  
  
 [向下切入至來自「採礦模型」的案例資料](drill-through-to-case-data-from-a-mining-model.md)。  
  
 如果在處理採礦結構時快取定型案例，而且您有必要的權限，您就可以從模型案例和採礦結構傳回資訊，包括沒有包含在採礦模型中的資料行。  
  
##  <a name="bkmk_DMX"></a>使用 DMX 建立鑽取查詢  
 如果您有模型或結構的權限，可以透過建立 DMX 查詢來鑽研案例資料。 如需以 DMX 建立鑽研查詢的語法範例，請參閱下列主題：  
  
 [使用 DMX 建立鑽研查詢](create-drillthrough-queries-using-dmx.md)  
  
##  <a name="bkmk_Considerations"></a>使用鑽取時的考慮  
  
-   如果您使用資料採礦精靈，啟用鑽研模型案例的選項位於精靈的最後一頁。 根據預設，系統會停用鑽研。 如需詳細資訊，請參閱[正在完成精靈 &#40;資料採礦精靈&#41;](../completing-the-wizard-data-mining-wizard.md)。  
  
-   您可以在現有的採礦模型上加入鑽研的能力，但是如果您這樣做，就必須先重新處理模型，然後才能鑽研資料。  
  
-   鑽研藉由擷取處理採礦結構時快取之定型案例的相關資訊來運作。 因此，如果您要在處理結構之後，將 <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> 屬性變更為 `ClearAfterProcessing` 來清除快取的資料，鑽研將不會運作。 若要啟用結構資料行的鑽研功能，您必須將 <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> 屬性變更為 `KeepTrainingCases`，然後重新處理結構。  
  
-   如果採礦結構不允許鑽研，但是採礦模型允許，您就只能檢視模型案例的資訊，而無法檢視採礦結構的資訊。  
  
###  <a name="bkmk_Security"></a>鑽取的安全性問題  
 如果您想要向下切入到模型的結構案例，您必須確認這兩個[AllowDrillThrough](https://docs.microsoft.com/bi-reference/assl/properties/allowdrillthrough-element-assl)屬性都設定為`True`。 此外，您必須是針對結構和模型同時擁有鑽研權限之角色的成員。 如需如何建立角色的資訊，請參閱[角色設計工具 &#40;Analysis Services - 多維度資料&#41;](https://msdn.microsoft.com/library/ms189696(v=sql.120).aspx)。 請參閱。  
  
 鑽研權限是在結構和模型上分別設定的。 即使您沒有結構的權限，模型權限還是可以讓您從模型進行鑽研。 結構的鑽研權限可以使用 [StructureColumn &#40;DMX&#41;](/sql/dmx/structurecolumn-dmx) 函數，提供將結構資料行從模型加入到鑽研查詢的額外功能。  
  
> [!NOTE]  
>  如果您在採礦結構和採礦模型上都啟用鑽研，則任何使用者 (針對採礦模型具有鑽研權限之角色的成員) 也可以檢視採礦結構中的資料行，即使這些資料行未包含在採礦模型中也一樣。 因此，若要保護機密資料，您應該設定資料來源檢視來遮罩個人資訊，並只有在必要時才允許採礦結構的鑽研存取。  
  
###  <a name="bkmk_Limits"></a>鑽取的限制  
  
-   下列限制會套用至模型的鑽研作業，端視用來建立模型的演算法而定：  
  
|演算法名稱|問題|  
|--------------------|-----------|  
|Microsoft 貝氏機率分類演算法|不支援。 這些演算法不會將案例指派給內容中的特定節點。|  
|Microsoft 類神經網路演算法|不支援。 這些演算法不會將案例指派給內容中的特定節點。|  
|Microsoft 羅吉斯迴歸演算法|不支援。 這些演算法不會將案例指派給內容中的特定節點。|  
|Microsoft 線性迴歸演算法|支援。 不過，由於此模型會建立單一節點 `All`，因此鑽研會傳回模型的所有培訓案例。 如果定型集很龐大，載入結果的時間可能會很長。|  
|Microsoft 時間序列演算法|支援。 不過，您無法使用資料採礦設計師中的 **[採礦模型檢視器]** ，鑽研結構或案例資料。 您必須改為建立 DMX 查詢。<br /><br /> 此外，您無法鑽研至特定節點，或撰寫 DMX 查詢來擷取時間序列模型之特定節點中的案例。 您可以使用其他準則 (例如日期或屬性值)，從模型或結構內部擷取案例資料。<br /><br /> 您也可以使用 [Lag &#40;DMX&#41;](/sql/dmx/lag-dmx) 函數來傳回模型中案例的日期。<br /><br /> 如果您想要檢視 Microsoft 時間序列演算法所建立之 ARTXP 和 ARIMA 節點的詳細資料，可以使用 [Microsoft 一般內容樹狀檢視器 &#40;資料採礦&#41;](../microsoft-generic-content-tree-viewer-data-mining.md)。|  
  
##  <a name="bkmk_Tasks"></a> 相關工作  
 使用下列連結，在特定案例中使用鑽研。  
  
|Task|連結|  
|----------|----------|  
|描述在資料採礦設計師中使用鑽研的程序|[鑽研採礦模型的案例資料](drill-through-to-case-data-from-a-mining-model.md)|  
|改變現有的採礦模型以允許鑽研|[針對採礦模型啟用鑽研](enable-drillthrough-for-a-mining-model.md)|  
|使用 DMX WITH DRILLTHROUGH 子句，在採礦結構上啟用鑽研|[&#40;DMX&#41;建立採礦結構](/sql/dmx/create-mining-structure-dmx)|  
|如需有關指派套用至採礦結構和採礦模型之權限的詳細資訊|[授與資料採礦結構和模型的許可權 &#40;Analysis Services&#41;](../multidimensional-models/grant-permissions-on-data-mining-structures-and-models-analysis-services.md)|  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦模型檢視器](data-mining-model-viewers.md)   
 [資料採礦查詢](data-mining-queries.md)  
  
  
