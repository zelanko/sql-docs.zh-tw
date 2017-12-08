---
title: "SystemGetClusterCrossValidationResults (Analysis Services-資料採礦) |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SystemGetClusterCrossValidationResults
- stored procedures [Analysis Services], data mining
- cross-validation [data mining]
ms.assetid: 79de9b81-9f2e-4f20-ace9-e3b19d6a9759
caps.latest.revision: "21"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: a741805b22296232bffdc881ba4105243ea92506
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="systemgetclustercrossvalidationresults-analysis-services---data-mining"></a>SystemGetClusterCrossValidationResults (Analysis Services - 資料採礦)
  將採礦結構分割成指定數目的交叉區段、定型每一個資料分割的模型，然後傳回每一個資料分割的精確度度量。  
  
 **注意** ：這個預存程序只能搭配至少包含一個叢集模型的採礦結構使用。 若要交叉驗證非叢集模型，您必須使用 [SystemGetCrossValidationResults &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
SystemGetClusterCrossValidationResults(  
<structure name>,   
[,<mining model list>]  
,<fold count>}  
,<max cases>  
<test list>])  
```  
  
## <a name="arguments"></a>引數  
 *採礦結構*  
 目前資料庫中的採礦結構名稱。  
  
 (必要)  
  
 *採礦模型清單*  
 要驗證之採礦模型的逗號分隔清單。  
  
 如果未指定採礦模型清單，將會針對與指定之結構有關的所有群集模型執行交叉驗證。  
  
> [!NOTE]  
>  若要交叉驗證非叢集模型的模型，您必須使用個別的預存程序 [SystemGetCrossValidationResults &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)。  
  
 (選擇性)  
  
 *摺疊計數*  
 指定要將資料集分成的資料分割數目的整數。 最小值為 2。 摺疊的最大數目為 **最大整數** 或是案例數，以較低者為準。  
  
 每一個資料分割都大概包含這個案例數： *最大案例數*/*摺疊計數*。  
  
 沒有預設值。  
  
> [!NOTE]  
>  摺疊數會大幅影響執行交叉驗證所需的時間。 如果您選取的數字太高，查詢可能會執行很長的一段時間，而在某些情況下可能會造成伺服器沒有回應或逾時。  
  
 (必要)  
  
 *最大案例數*  
 指定可以測試之最大案例數的整數。  
  
 0 的值表示將會使用資料來源內的所有案例。  
  
 如果您指定的數字高於資料集內的實際案例數，就會使用資料來源內的所有案例。  
  
 (必要)  
  
 *測試清單*  
 指定測試選項的字串。  
  
 **注意** ：這個參數保留給未來使用。  
  
 (選擇性)  
  
## <a name="return-type"></a>傳回類型  
 傳回類型資料表包含每一個個別資料分割的分數及所有模型的彙總。  
  
 下表描述傳回的資料行。  
  
|資料行名稱|說明|  
|-----------------|-----------------|  
|ModelName|已測試的模型名稱。|  
|AttributeName|可預測的資料行名稱。 若為叢集模型，一律為 **null**。|  
|AttributeState|可預測資料行內的指定目標值。 若為叢集模型，一律為 **null.**|  
|PartitionIndex|以 1 為基準的索引，可識別套用結果的資料分割。|  
|PartitionSize|指示每一個資料分割內包含了多少案例數的整數。|  
|測試|已執行的測試類型。|  
|[量值]|測試所傳回之量值的名稱。 每一個模型的量值都取決於可預測值的類型。 如需每個量值的定義，請參閱[交叉驗證 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md)。<br /><br /> 如需每一個可預測類型所傳回的量值清單，請參閱[交叉驗證報表中的量值](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md)。|  
|Value|指定之測試量值的值。|  
  
## <a name="remarks"></a>備註  
 若要傳回整個資料集的精確度度量，請使用 [SystemGetClusterAccuracyResults &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)。  
  
 此外，如果採礦模型已經分割成若干摺疊，您可以使用 [SystemGetClusterAccuracyResults &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)。  
  
## <a name="examples"></a>範例  
 下列範例示範如何將採礦結構分割成三個摺疊，然後測試與此採礦結構有關的兩個群集模型。  
  
 程式碼的第三行會列出您想要測試的特定採礦模型。 如果您未指定此清單，便會使用與此結構有關的所有群集模型。  
  
 程式碼的第四行指定摺疊的數目，第五行則指定要使用的最大案例數。  
  
 因為這些是群集模型，所以您不需要指定可預測的屬性或值。  
  
```  
CALL SystemGetClusterCrossValidationResults(  
[v Target Mail],  
[Cluster 1], [Cluster 2],  
3,  
10000  
)  
```  
  
 範例結果：  
  
|ModelName|AttributeName|AttributeState|PartitionIndex|PartitionSize|測試|[量值]|Value|  
|---------------|-------------------|--------------------|--------------------|-------------------|----------|-------------|-----------|  
|叢集 1|||1|3025|群集|案例概似值|0.930524511864121|  
|叢集 1|||2|3025|群集|案例概似值|0.919184178430778|  
|叢集 1|||3|3024|群集|案例概似值|0.929651120490248|  
|群集 2|||1|1289|群集|案例概似值|0.922789726933607|  
|群集 2|||2|1288|群集|案例概似值|0.934865535691068|  
|群集 2|||3|1288|群集|案例概似值|0.924724595688798|  
  
## <a name="requirements"></a>需求  
 從 [!INCLUDE[ssEnterprise](../../includes/ssenterprise-md.md)] 開始，交叉驗證只能在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]中使用。  
  
## <a name="see-also"></a>請參閱＜  
 [SystemGetCrossValidationResults &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetAccuracyResults &#40;Analysis Services-資料採礦 &#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)   
 [SystemGetClusterCrossValidationResults](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetClusterAccuracyResults &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)  
  
  
