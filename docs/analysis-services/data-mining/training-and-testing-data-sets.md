---
title: "定型和測試資料集 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- testing mining models
- holdout [data mining]
- testing data mining models
- accuracy testing [data mining]
ms.assetid: 5798fa48-ef3c-4e97-a17c-38274970fccd
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9465d0eda4b15827cf20c4b9579a5eff672ce1d1
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="training-and-testing-data-sets"></a>定型和測試資料集
  將資料分成定型集和測試集是評估資料採礦模型中的一個重要部分。 一般來說，當您將資料集分成定型集和測試集時，大多數的資料會用於定型，小部分的資料會用於測試。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會隨機取樣資料，以確保測試集和定型集類似。 您可以透過針對定型和測試使用相同的資料，盡可能減少資料不一致的影響並有效了解模型的特性。  
  
 在使用定型集處理過模型之後，您可以針對測試集進行預測來測試模型。 由於測試集中的資料已經包含您想要預測之屬性的已知值，所以可以輕鬆地判斷模型的猜測是否正確。  
  
## <a name="creating-test-and-training-sets-for-data-mining-structures"></a>為資料採礦結構建立測試集和定型集  
 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中，您可以分隔位於採礦結構層級的原始資料集。 有關定型和測試資料集的大小資訊，以及這兩個資料集中所含之資料列的詳細資訊，會與結構一起儲存，而且以該結構為基礎的所有模型都可以使用這些資料集進行定型和測試。  
  
 您可以利用下列方式，針對採礦結構定義測試資料集：  
  
-   在您建立採礦結構時，使用 [資料採礦精靈] 來分割採礦結構。  
  
-   在資料採礦設計師的 **[採礦結構]** 索引標籤中修改結構屬性。  
  
-   透過使用分析管理物件 (AMO) 或 XML 資料定義語言 (DDL)，以程式設計方式建立和修改結構。  
  
### <a name="using-the-data-mining-wizard-to-divide-a-mining-structure"></a>使用資料採礦精靈來分割採礦結構  
 根據預設，當您定義了採礦結構的資料來源之後，[資料採礦精靈] 會將資料分成兩個集合：其中一個集合具有 70% 的來源資料，用於定型模型；而另一個集合具有 30% 的來源資料，用於測試模型。 選擇此預設值是因為資料採礦通常使用 70-30 的比例，但是透過 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ，您可以變更此比例以符合您的需求。  
  
 此外，您可以設定精靈以便設定定型案例的最大數目，也可以結合限制以便允許案例的最大百分比 (最高達指定的最大案例數目)。 當您同時指定案例的最大百分比和案例的最大數目時， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會使用這兩個限制中的較小者當做測試集的大小。 例如，如果您針對測試案例指定 30% 鑑效組，而且測試案例的最大數目為 1000，則測試集的大小絕對不會超過 1000 個案例。 如果您想要確保測試集的大小維持一致 (即使有更多定型資料加入至模型)，這可能會很有用。  
  
 如果您針對不同的採礦結構使用相同的資料來源檢視，並想確保所有採礦結構及其模型使用大致相同的方式分割資料，您應該指定用來初始化隨機取樣的種子。 當您指定 **HoldoutSeed**的值時， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 將使用該值來開始取樣。 否則，取樣會針對採礦結構的名稱使用雜湊演算法來建立初始值。  
  
> [!NOTE]  
>  如果使用 **EXPORT** 和 **IMPORT** 陳述式建立採礦結構的複本，由於匯出程序建立新識別碼但使用相同名稱，因此新採礦結構會有相同的定型和測試資料集。 不過，如果兩個採礦結構使用相同的基礎資料來源，但具有不同的名稱，則針對每個採礦結構所建立的集合將會不同。  
  
### <a name="modifying-structure-properties-to-create-a-test-data-set"></a>修改結構屬性以建立測試資料集  
 如果您建立並處理採礦結構，然後決定要保留測試資料集，您可以修改採礦結構的屬性。 若要變更資料分割的方式，請編輯下列屬性：  
  
|屬性|說明|  
|--------------|-----------------|  
|**HoldoutMaxCases**|指定測試集中要包含的最大案例數目。|  
|**HoldoutMaxPercent**|將測試集中要包含的案例數目指定為完整資料集的百分比。 如果沒有任何資料集，您應該指定 0。|  
|**HoldoutSeed**|指定一個整數值，以便在隨機選取資料分割的資料時當做種子使用。 這個值不會影響定型集中的案例數目。不過，它會確保資料分割可重複。|  
  
 如果您在現有的結構中加入或變更測試資料集，就必須重新處理結構和所有相關聯的模型。 此外，由於分割來源資料會導致模型針對不同的資料子集進行定型，因此您可能會看見模型產生不同的結果。  
  
### <a name="specifying-holdout-programmatically"></a>以程式設計方式指定鑑效組  
 您可以使用 DMX 陳述式、AMO 或 XML DDL 來定義採礦結構的測試和定型資料集。 ALTER MINING STRUCTURE 陳述式不支援使用鑑效組參數。  
  
-   **DMX** ：在資料採礦延伸模組 (DMX) 語言中，CREATE MINING STRUCTURE 陳述式已經擴充成包含 WITH HOLDOUT 子句。  
  
-   **ASSL** ：您可以使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 指令碼語言 (ASSL)，藉以建立新的採礦結構，或將測試資料集加入至現有的採礦結構。  
  
-   **AMO** ：您也可以使用 AMO 來檢視和修改鑑效組資料集。  
  
 您可以查詢資料採礦結構描述資料列集，以檢視現有採礦結構中有關鑑效組資料集的詳細資訊。 您可以發出 DISCOVER ROWSET 呼叫來進行這項處理，或是使用 DMX 查詢。  
  
## <a name="retrieving-information-about-holdout-data"></a>擷取鑑效組資料的資訊  
 預設會快取定型和測試資料集的所有資訊，讓您可以使用現有的資料來定型然後測試新的模型。 您也可以定義要套用至快取鑑效組資料的篩選，如此您就可以評估資料子集的模型。  
  
 案例分成若干定型和測試資料集的方式取決於您設定鑑效組的方式以及您提供的資料。 如果您想要判斷用於定型或測試的案例數目，或想要找出有關定型集和測試集中包含之案例的其他詳細資料，您可以建立 DMX 查詢來查詢模型結構。 例如，下列查詢會傳回模型之定型集中使用的案例。  
  
```  
SELECT * from <structure>.CASES WHERE IsTrainingCase()  
```  
  
 若只要擷取測試案例，並額外針對採礦結構中的其中一個資料行篩選測試案例，請使用下列語法：  
  
```  
SELECT * from <structure>.CASES WHERE IsTestCase() AND <structure column name> = '<value>'  
```  
  
## <a name="limitations-on-the-use-of-holdout-data"></a>使用鑑效組資料的限制  
  
-   若要使用鑑效組，<xref:Microsoft.AnalysisServices.MiningStructureCacheMode>採礦結構的屬性必須設定為預設值， **KeepTrainingCases**。 如果您將 **CacheMode** 屬性變更為 **ClearAfterProcessing**，然後重新處理採礦結構，資料分割將會遺失。  
  
-   您無法從時間序列模型中移除資料；因此，您無法將來源資料分成定型集和測試集。 如果您開始建立採礦結構和模型，並選擇 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 時間序列演算法，即會停用建立鑑效組資料集的選項。 如果採礦結構在案例或巢狀資料表層級包含 KEY TIME 資料行，也會停用鑑效組資料。  
  
-   您可能會不小心設定鑑效組資料集使用完整資料集進行測試，而沒有保留任何資料給定型。 但是，如果發生此情況， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 將會引發錯誤，以便讓您更正問題。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 也會在處理結構時警告您。  
  
-   在大部分情況下，預設的鑑效組值 30 會在定型與測試資料之間提供良好的平衡。 目前沒有任何簡易方式可判斷資料集應該設定為多大才能提供足夠的定型，或定型集可設定為多疏鬆，而仍能避免過度學習。 但是，在您建立模型之後，可以使用交叉驗證來評估與特定模型相關的資料集。  
  
-   除了上表所列的屬性以外，AMO 和 XML DDL 中也提供了一個唯讀屬性 **HoldoutActualSize**。 不過，由於資料分割的實際大小要等到結構已經處理之後才能正確判斷出，因此您應該先檢查模型是否已經處理，然後再擷取 **HoldoutActualSize** 屬性的值。  
  
## <a name="related-content"></a>相關內容  
  
|主題|連結|  
|------------|-----------|  
|描述模型上的篩選與定型和測試資料集的互動方式。|[採礦模型的篩選 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)|  
|描述定型和測試資料的使用如何影響交叉驗證。|[交叉驗證 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md)|  
|提供有關使用採礦結構中的定型集和測試集之程式設計介面的詳細資訊。|[AMO 概念和物件模型](../../analysis-services/multidimensional-models/analysis-management-objects/amo-concepts-and-object-model.md)<br /><br /> [MiningStructure 元素 &#40;ASSL&#41;](../../analysis-services/scripting/objects/miningstructure-element-assl.md)|  
|提供用於建立鑑效組資料集的 DMX 語法。|[CREATE MINING STRUCTURE &#40;DMX&#41;](../../dmx/create-mining-structure-dmx.md)|  
|擷取有關定型集和測試集中案例的資訊。|[資料採礦結構描述資料列集](../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)<br /><br /> [資料採礦結構描述資料列集 &#40;SSA&#41;](../../analysis-services/data-mining/data-mining-schema-rowsets-ssas.md)|  
  
## <a name="see-also"></a>請參閱＜  
 [資料採礦工具。](../../analysis-services/data-mining/data-mining-tools.md)   
 [資料採礦概念](../../analysis-services/data-mining/data-mining-concepts.md)   
 [資料採礦方案](../../analysis-services/data-mining/data-mining-solutions.md)   
 [測試及驗證 &#40;資料採礦&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md)  
  
  

