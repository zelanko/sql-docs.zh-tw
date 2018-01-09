---
title: "SystemGetAccuracyResults (Analysis Services-資料採礦) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- stored procedures [Analysis Services], data mining
- SystemGetAccuracyResults
- cross-validation [data mining]
ms.assetid: 54ff584c-c6ce-4c31-9515-0a645719bd1a
caps.latest.revision: "26"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 1f6cc8a8bc3e35f6072e5998faed8fb9d51b768f
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="systemgetaccuracyresults-analysis-services---data-mining"></a>SystemGetAccuracyResults (Analysis Services - 資料採礦)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]傳回採礦結構和所有相關的模型，不包括群集模型的交叉驗證精確度標準。  
  
 此預存程序會將整組資料的度量當做單一資料分割來傳回。 若要將資料集分割成交叉區段，並傳回每個資料分割的度量，請使用 [SystemGetCrossValidationResults &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)。  
  
> [!NOTE]  
>  如果是使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 時間序列演算法或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 時序群集演算法所建立的模型，則不支援這個預存程序。 此外，針對群集模型，請使用不同的預存程序， [SystemGetClusterAccuracyResults &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
SystemGetAccuracyResults(<mining structure>,   
[,<mining model list>]  
,<data set>  
,<target attribute>  
[,<target state>]  
[,<target threshold>]  
[,<test list>])  
```  
  
## <a name="arguments"></a>引數  
 *採礦結構*  
 目前資料庫中的採礦結構名稱。  
  
 (必要)  
  
 *模型清單*  
 要驗證之模型的逗號分隔清單。  
  
 預設值是 **null**。 這表示會使用所有適用的模型。 當使用預設值時，將會自動從候選清單中排除要處理的群集模型。  
  
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
  
 *目標屬性*  
 包含可預測之物件名稱的字串。 可預測的物件可以是資料行、巢狀資料表資料行，或是採礦模型的巢狀資料表索引鍵資料行。  
  
 (必要)  
  
 *目標狀態*  
 包含要預測之特定值的字串。  
  
 如果指定了某個值，將會根據該特定狀態來收集度量。  
  
 如果未指定任何值，或是指定了 null，將會針對每一項預測最有可能的狀態來計算度量。  
  
 預設值是 **null**。  
  
 (選擇性)  
  
 *目標臨界值*  
 介於 0.0 和 1 之間的數字，可指定預測值算為正確的最低機率。  
  
 預設值是 **null**，這表示所有預測都會算為正確。  
  
 (選擇性)  
  
 *測試清單*  
 指定測試選項的字串。 這個參數保留給未來使用。  
  
 (選擇性)  
  
## <a name="return-type"></a>傳回類型  
 傳回的資料列集包含每一個資料分割的分數及所有模型的彙總。  
  
 下表列出 **GetValidationResults**傳回的資料行。  
  
|資料行名稱|描述|  
|-----------------|-----------------|  
|[模型]|已測試的模型名稱。 [全部] 表示結果是所有模型的彙總。|  
|AttributeName|可預測的資料行名稱。|  
|AttributeState|可預測資料行內的目標值。<br /><br /> 如果這個資料行包含值，只會針對指定的狀態收集度量。<br /><br /> 如果未指定這個值，或是指定了 null，將會針對每一項預測最有可能的狀態來計算度量。|  
|PartitionIndex|代表套用結果的磁碟分割。<br /><br /> 對於此程序而言，一定是 0。|  
|PartitionCases|整數，表示在案例集，根據資料列數目*\<資料集 >*參數。|  
|測試|已執行的測試類型。|  
|[量值]|測試所傳回之量值的名稱。 每一個模型的量值取決於模型類型及可預測值的類型。<br /><br /> 如需每一個可預測類型所傳回的量值清單，請參閱[交叉驗證報表中的量值](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md)。<br /><br /> 如需每個量值的定義，請參閱[交叉驗證 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md)。|  
|ReplTest1|指定之量值的值。|  
  
## <a name="remarks"></a>備註  
 下表提供您可以在用於交叉驗證的採礦結構內指定資料的值範例。 如果您想要將測試案例用於交叉驗證，採礦結構必須已經包含測試資料集。 如需在建立採礦結構時如何定義測試資料集的相關資訊，請參閱 [定型和測試資料集](../../analysis-services/data-mining/training-and-testing-data-sets.md)。  
  
|整數值|描述|  
|-------------------|-----------------|  
|@shouldalert|只會使用定型案例。|  
|2|只會使用測試案例。|  
|3|定型案例和測試案例都會使用。|  
|4|組合無效。|  
|5|只會使用定型案例，而且會套用模型篩選器。|  
|6|只會使用測試案例，而且會套用模型篩選器。|  
|7|定型案例和測試案例都會使用，而且會套用模型篩選器。|  
  
 如需您將使用交叉驗證之案例的詳細資訊，請參閱[測試和驗證 &#40;資料採礦&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md)。  
  
## <a name="examples"></a>範例  
 此範例會針對單一決策樹模型 `v Target Mail DT`(與 `vTargetMail` 採礦結構有關) 傳回精確度的量值。 第四行的程式碼指示結果應該根據測試案例，由每一個模型特有的篩選器來針對該模型進行篩選。  `[Bike Buyer]` 會指定要預測的資料行，而下一行的 1 指示此模型只會針對特定值 1 來預估，表示「是的，將會購買」。  
  
 程式碼的最後一行指定狀態臨界值為 0.5。 這表示在計算精確度時，機率大於百分之 50 的預測應該算為「良好」預測。  
  
```  
CALL SystemGetAccuracyResults (  
[vTargetMail],  
[vTargetMail DT],  
6,  
'Bike Buyer',  
1,  
0.5  
)  
```  
  
 範例結果：  
  
|ModelName|AttributeName|AttributeState|PartitionIndex|PartitionSize|測試|量值|ReplTest1|  
|---------------|-------------------|--------------------|--------------------|-------------------|----------|-------------|-----------|  
|v Target Mail DT|Bike Buyer|@shouldalert|0|1638|分類|真肯定|605|  
|v Target Mail DT|Bike Buyer|@shouldalert|0|1638|分類|誤判|177|  
|v Target Mail DT|Bike Buyer|@shouldalert|0|1638|分類|真否定|501|  
|v Target Mail DT|Bike Buyer|@shouldalert|0|1638|分類|誤否定|355|  
|v Target Mail DT|Bike Buyer|@shouldalert|0|1638|可能性|對數分數|-0.598454638753028|  
|v Target Mail DT|Bike Buyer|@shouldalert|0|1638|可能性|增益|0.0936717116894395|  
|v Target Mail DT|Bike Buyer|@shouldalert|0|1638|可能性|均方根誤差|0.361630800104946|  
  
## <a name="requirements"></a>需求  
 從 [!INCLUDE[ssEnterprise](../../includes/ssenterprise-md.md)] 開始，交叉驗證只能在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]中使用。  
  
## <a name="see-also"></a>請參閱  
 [SystemGetCrossValidationResults &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetAccuracyResults](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)   
 [SystemGetClusterCrossValidationResults &#40;Analysis Services-資料採礦 &#41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetClusterAccuracyResults &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)  
  
  
