---
title: SystemGetClusterAccuracyResults (Analysis Services-資料採礦) |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b9521cfd6e2b9ec0d08f290c60167c682c98e46f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "68209657"
---
# <a name="systemgetclusteraccuracyresults-analysis-services---data-mining"></a>SystemGetClusterAccuracyResults (Analysis Services - 資料採礦)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  針對採礦結構和所有相關的叢集模型傳回交叉驗證精確度的度量。  
  
 此預存程序會將整個資料集的度量當做單一資料分割來傳回。 若要將資料集分割成交叉區段，並傳回每個資料分割的度量，請使用 [SystemGetClusterCrossValidationResults &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)。  
  
> [!NOTE]  
>  這個預存程序只適用於群集模型。 對於非叢集模型，請使用 [SystemGetAccuracyResults &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
SystemGetClusterAccuracyResults(  
<mining structure>   
[,<mining model list>]  
,<data set>  
,<test list>])  
```  
  
## <a name="arguments"></a>引數  
 *採礦結構*  
 目前資料庫中的採礦結構名稱。  
  
 (必要)  
  
 *採礦模型清單*  
 要驗證之模型的逗號分隔清單。  
  
 預設值是 **null**，表示會使用所有適用的模型。 當使用預設值時，將會自動從候選清單中排除要處理的非叢集模型。  
  
 (選擇性)  
  
 *資料集*  
 指出採礦結構中哪一個資料分割要用於測試的整數值。 此值衍生自代表下列值總和的位元遮罩，其中任何單一值都是選擇性：  
  
|||  
|-|-|  
|定型案例|0x0001|  
|測試案例|0x0002|  
|模型篩選器|0x0004|  
  
 如需可能值的完整清單，請參閱本主題的「備註」一節。  
  
 (必要)  
  
 *測試清單*  
 指定測試選項的字串。 這個參數保留給未來使用。  
  
 (選擇性)  
  
## <a name="return-type"></a>傳回類型  
 包含每一個個別資料分割之分數及所有模型之彙總的資料表。  
  
 下表列出 **SystemGetClusterAccuracyResults**所傳回的資料行。 若要深入了解如何解譯預存程序所傳回資訊的詳細資訊，請參閱 [交叉驗證報表中的量值](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md)。  
  
|資料行名稱|描述|  
|-----------------|-----------------|  
|ModelName|已測試的模型名稱。 [全部]  表示結果是所有模型的彙總。|  
|AttributeName|不適用於叢集模型。|  
|AttributeState|不適用於叢集模型。|  
|PartitionIndex|指示資料分割的數字。<br /><br /> 對於這個預存程序而言，此數字一定是 0。|  
|PartitionCases|指示已經測試了多少案例的整數。|  
|測試|已執行的測試類型。|  
|[量值]|測試所傳回之量值的名稱。 每一個模型的量值取決於模型類型及可預測值的類型。<br /><br /> 如需每一個可預測類型所傳回的量值清單，請參閱[交叉驗證報表中的量值](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md)。<br /><br /> 如需每個量值的定義，請參閱[交叉驗證 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md)。|  
|值|指示群集案例可能性的機率分數。|  
  
## <a name="remarks"></a>備註  
 下表提供您可以在用於交叉驗證的採礦結構內指定資料的值範例。 如果您想要將測試案例用於交叉驗證，採礦結構必須已經包含測試資料集。 如需在建立採礦結構時如何定義測試資料集的相關資訊，請參閱 [定型和測試資料集](../../analysis-services/data-mining/training-and-testing-data-sets.md)。  
  
|整數值|描述|  
|-------------------|-----------------|  
|1|只會使用定型案例。|  
|2|只會使用測試案例。|  
|3|定型案例和測試案例都會使用。|  
|4|組合無效。|  
|5|只會使用定型案例，而且會套用模型篩選器。|  
|6|只會使用測試案例，而且會套用模型篩選器。|  
|7|定型案例和測試案例都會使用，而且會套用模型篩選器。|  
  
 如需您將使用交叉驗證之案例的詳細資訊，請參閱[測試和驗證 &#40;資料採礦&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md)。  
  
## <a name="examples"></a>範例  
 此範例會傳回兩個叢集模型 (名為 `Cluster 1` 和 `Cluster 2`) 的精確度量值 (這兩個模型與 vTargetMail 採礦結構有關)。 第四行程式碼指示結果應該只根據測試案例，而不使用任何可能與每一個模型有關的篩選。  
  
```  
CALL SystemGetClusterAccuracyResults (  
[vTargetMail],  
[Cluster 1], [Cluster 2],  
2  
)  
```  
  
 範例結果：  
  
|ModelName|AttributeName|AttributeState|PartitionIndex|PartitionSize|測試|[量值]|值|  
|---------------|-------------------|--------------------|--------------------|-------------------|----------|-------------|-----------|  
|叢集 1|||0|5545|群集|案例概似值|0.796514342249313|  
|群集 2|||0|5545|群集|案例概似值|0.732122471228572|  
  
## <a name="requirements"></a>需求  
 從 [!INCLUDE[ssEnterprise](../../includes/ssenterprise-md.md)] 開始，交叉驗證只能在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]中使用。  
  
## <a name="see-also"></a>另請參閱  
 [SystemGetCrossValidationResults &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetAccuracyResults &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)   
 [SystemGetClusterCrossValidationResults &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)   
 [SystemClusterGetAccuracyResults](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)  
  
  
