---
title: "使用 DMX 建立鑽研查詢 |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 42c896ee-e5ee-4017-b66e-31d1fe66d369
caps.latest.revision: 5
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 93a6893146a2367719ad7b4bed23a76b7d43e589
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="create-drillthrough-queries-using-dmx"></a>使用 DMX 建立鑽研查詢
  對於支援鑽研的所有模型，您可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或支援 DMX 的任何其他用戶端中建立 DMX 查詢，藉以擷取案例資料和結構資料。  
  
> [!WARNING]  
>  若要檢視這些資料，必須已啟用鑽研，而且您必須擁有必要的權限。  
  
## <a name="specifying-drillthrough-options"></a>指定鑽研選項  
 擷取模型案例和結構案例的一般語法如下：  
  
```  
SELECT <model column list>, StructureColumn('<structure column name') FROM <modelname>.CASES  
```  
  
 如需使用 DMX 查詢來傳回案例資料的詳細資訊，請參閱 [SELECT FROM &#60;模型&#62;.CASES &#40;DMX&#41;](../../dmx/select-from-model-cases-dmx.md) 和 [SELECT FROM &#60;結構&#62;.CASES](../../dmx/select-from-structure-cases.md)。  
  
## <a name="examples"></a>範例  
 下列 DMX 查詢會從時間序列模型中傳回特定產品序列的案例資料。 此查詢也會傳回模型中沒有使用，但採礦結構中有提供的 **Amount**資料行。  
  
```  
SELECT [DateSeries], [Model Region], Quantity, StructureColumn('Amount') AS [M200 Pacific Amount]  
FROM Forecasting.CASES  
WHERE [Model Region] = 'M200 Pacific'  
```  
  
 請注意，在這則範例中，別名已用來重新命名結構資料行。 如果您沒有指派別名給結構資料行，就會傳回名為 'Expression' 的資料行。 這是所有未命名資料行的預設行為。  
  
## <a name="see-also"></a>請參閱＜  
 [鑽研查詢 &#40;資料採礦&#41;](../../analysis-services/data-mining/drillthrough-queries-data-mining.md)   
 [採礦結構的鑽研](../../analysis-services/data-mining/drillthrough-on-mining-structures.md)  
  
  

