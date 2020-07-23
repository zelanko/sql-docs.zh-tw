---
title: 更新（DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f77d71eab284b695171e923cfe53b53575d45d94
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2020
ms.locfileid: "86971536"
---
# <a name="update-dmx"></a>UPDATE (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  變更資料採礦模型中的**NODE_CAPTION**資料行。  
  
## <a name="syntax"></a>語法  
  
```  
  
UPDATE <model>.CONTENT  
SET NODE_CAPTION='new caption'  
[WHERE <condition expression>]  
```  
  
## <a name="arguments"></a>引數  
 *model*  
 模型識別碼。  
  
 *新標題*  
 字串，其中包含**NODE_CAPTION**資料行的新名稱。  
  
 *條件運算式*  
 選擇性。 限制從資料行清單傳回之值的條件。  
  
## <a name="examples"></a>範例  
 在下列範例中， **UPDATE**語句會將叢集的預設名稱變更為 `Cluster 1` `001` 更具描述性的名稱 `Likely Customers` 。  
  
```  
UPDATE [TM Clustering].CONTENT  
SET NODE_CAPTION= 'Likely Customers'  
WHERE NODE_UNIQUE_NAME = '001'  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組 &#40;DMX&#41; 資料定義語句](../dmx/dmx-statements-data-definition.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 資料動作陳述式](../dmx/dmx-statements-data-manipulation.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 陳述式參考](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
