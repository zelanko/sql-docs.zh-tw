---
title: SystemGetCrossValidationResults (Analysis Services-資料採礦) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SystemGetCrossValidationResults
- stored procedures [Analysis Services], data mining
- cross-validation [data mining]
ms.assetid: f70c3337-c930-434a-b278-caf1ef0c3b3b
caps.latest.revision: 26
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ddb4255fb09131bb2612e47b44a0bedfc22e4be4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="systemgetcrossvalidationresults-analysis-services---data-mining"></a>SystemGetCrossValidationResults (Analysis Services - 資料採礦)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  將採礦結構分割成指定數目的交叉區段、定型每一個資料分割的模型，然後傳回每一個資料分割的精確度度量。  
  
> [!NOTE]  
>  這個預存程序無法用來交叉驗證使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 時間序列演算法或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 時序叢集演算法所建立的叢集模型或模型。 若要交叉驗證叢集模型，您可以使用個別的預存程序 [SystemGetClusterCrossValidationResults &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
SystemGetCrossValidationResults(  
<mining structure>  
[, <mining model list>]  
,<fold count>  
,<max cases>  
,<target attribute>  
[,<target state>]  
[,<target threshold>]  
[,<test list>])  
```  
  
## <a name="arguments"></a>引數  
 *採礦結構*  
 目前資料庫中的採礦結構名稱。  
  
 (必要)  
  
 *採礦模型清單*  
 要驗證之採礦模型的逗號分隔清單。  
  
 如果模型名稱包含任何在識別碼名稱中無效的字元，該名稱必須加上方括號。  
  
 如果未指定採礦模型清單，將會針對與指定之結構有關且包含可預測屬性的所有模型，執行交叉驗證。  
  
> [!NOTE]  
>  若要交叉驗證叢集模型，您必須使用個別的預存程序 [SystemGetClusterCrossValidationResults &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)。  
  
 (選擇性)  
  
 *摺疊計數*  
 指定要將資料集分成的資料分割數目的整數。 最小值為 2。 摺疊的最大數目為 **最大整數** 或是案例數，以較低者為準。  
  
 每一個資料分割都大概包含這個案例數： *最大案例數*/*摺疊計數*。  
  
 沒有預設值。  
  
> [!NOTE]  
>  摺疊數會大幅影響執行交叉驗證所需的時間。 如果您選取的數字太高，查詢可能會執行很長的一段時間，而在某些情況下可能會造成伺服器沒有回應或逾時。  
  
 (必要)  
  
 *最大案例數*  
 指定可以在所有摺疊中測試之最大案例數的整數。  
  
 0 的值表示將會使用資料來源內的所有案例。  
  
 如果您指定的值大於資料集內的實際案例數，就會使用資料來源內的所有案例。  
  
 沒有預設值。  
  
 (必要)  
  
 *目標屬性*  
 包含可預測屬性之名稱的字串。 可預測屬性可以是資料行、巢狀資料表資料行，或是採礦模型的巢狀資料表索引鍵資料行。  
  
> [!NOTE]  
>  只會在執行階段驗證目標屬性是否存在。  
  
 (必要)  
  
 *目標狀態*  
 指定要預測之值的公式。 如果指定了目標值，就只會針對指定的值來收集度量。  
  
 如果未指定值，或指定 **null**，將會針對每一項預測最有可能的狀態來計算度量。  
  
 預設值是 **null**。  
  
 如果指定的值對於指定的屬性無效，或是此公式對於指定的屬性而言不是正確的類型，驗證期間就會引發錯誤。  
  
 (選擇性)  
  
 *目標*  *臨界值*  
 **Double** 大於 0 且小於 1。 指示要將指定之目標狀態的預測所必須取得的最小機率分數算為正確的。  
  
 機率小於或等於這個值的預測會被視為不正確。  
  
 如果未指定任何值或者為 **null**，就會使用最可能的狀態，不論它的機率分數為何。  
  
 預設值是 **null**。  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 如果您將不會引發錯誤*狀態臨界值*為 0.0，但您應該永遠不會使用此值。 就實際而言，0.0 的臨界值表示機率百分之 0 的預測將會算為正確的。  
  
 (選擇性)  
  
 *測試清單*  
 指定測試選項的字串。  
  
 **注意** ：這個參數保留給未來使用。  
  
 (選擇性)  
  
## <a name="return-type"></a>傳回類型  
 傳回的資料列集包含每一個模型內之每一個資料分割的分數。  
  
 下表描述此資料列集中的資料行。  
  
|資料行名稱|Description|  
|-----------------|-----------------|  
|ModelName|已測試的模型名稱。|  
|AttributeName|可預測的資料行名稱。|  
|AttributeState|可預測資料行內的指定目標值。 如果這個值是 **null**，表示已使用最有可能的預測。<br /><br /> 如果這個資料行包含值，就只會針對這個值來評估此模型的精確度。|  
|PartitionIndex|以 1 為基準的索引，可識別套用結果的資料分割。|  
|PartitionSize|指示每一個資料分割內包含了多少案例數的整數。|  
|測試|已執行之測試的類別目錄。 如需類別目錄以及包含在每一個類別目錄中之測試的描述，請參閱 [交叉驗證報表中的量值](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md)。|  
|[量值]|測試所傳回之量值的名稱。 每一個模型的量值都取決於可預測值的類型。 如需每個量值的定義，請參閱[交叉驗證 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md)。<br /><br /> 如需每一個可預測類型所傳回的量值清單，請參閱 [交叉驗證報表中的量值](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md)。|  
|Value|指定之測試量值的值。|  
  
## <a name="remarks"></a>備註  
 若要傳回整個資料集的精確度度量，請使用 [SystemGetAccuracyResults &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)。  
  
 如果採礦模型已經分割成若干摺疊，您可以使用 [SystemGetAccuracyResults &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)。  
  
## <a name="examples"></a>範例  
 下列範例示範如何將交叉驗證的採礦結構分割成兩個摺疊，然後測試與採礦結構 `[v Target Mail]`有關的兩個採礦模型。  
  
 程式碼的第三行會列出您想要測試的採礦模型。 如果您未指定此清單，便會使用與此結構有關的所有非叢集模型。 程式碼的第四行會指定資料分割數目。 因為未針對 *max cases*指定任何值，所以將會使用採礦結構中的所有案例，並在資料分割之間平均分配。  
  
 第五行指定可預測屬性 Bike Buyer，第六行則指定要預測的值 1 (表示「是的，將會購買」)。  
  
 第七行的 NULL 值表示，並沒有必須符合的最小機率限制。 因此，將會使用機率不是零的第一個預測來評估精確度。  
  
```  
CALL SystemGetCrossValidationResults(  
[v Target Mail],  
[Target Mail DT], [Target Mail NB],  
2,  
'Bike Buyer',  
1,  
NULL  
)  
```  
  
 範例結果：  
  
|ModelName|AttributeName|AttributeState|PartitionIndex|PartitionSize|測試|量值|Value|  
|---------------|-------------------|--------------------|--------------------|-------------------|----------|-------------|-----------|  
|Target Mail DT|Bike Buyer|1|1|500|分類|真肯定|144|  
|Target Mail DT|Bike Buyer|1|1|500|分類|誤判|105|  
|Target Mail DT|Bike Buyer|1|1|500|分類|真否定|186|  
|Target Mail DT|Bike Buyer|1|1|500|分類|誤否定|65|  
|Target Mail DT|Bike Buyer|1|1|500|可能性|對數分數|-0.619042807138345|  
|Target Mail DT|Bike Buyer|1|1|500|可能性|增益|0.0740963734002671|  
|Target Mail DT|Bike Buyer|1|1|500|可能性|均方根誤差|0.346946279977653|  
|Target Mail DT|Bike Buyer|1|2|500|分類|真肯定|162|  
|Target Mail DT|Bike Buyer|1|2|500|分類|誤判|86|  
|Target Mail DT|Bike Buyer|1|2|500|分類|真否定|165|  
|Target Mail DT|Bike Buyer|1|2|500|分類|誤否定|87|  
|Target Mail DT|Bike Buyer|1|2|500|可能性|對數分數|-0.654117781086519|  
|Target Mail DT|Bike Buyer|1|2|500|可能性|增益|0.038997399132084|  
|Target Mail DT|Bike Buyer|1|2|500|可能性|均方根誤差|0.342721344892651|  
  
## <a name="requirements"></a>需求  
 從 [!INCLUDE[ssEnterprise](../../includes/ssenterprise-md.md)] 開始，交叉驗證只能在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]中使用。  
  
## <a name="see-also"></a>另請參閱  
 [SystemGetCrossValidationResults](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetAccuracyResults &#40;Analysis Services-資料採礦&#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)   
 [SystemGetClusterCrossValidationResults &#40;Analysis Services-資料採礦&#41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetClusterAccuracyResults & #40;Analysis Services-資料採礦 & #41;](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)  
  
  
