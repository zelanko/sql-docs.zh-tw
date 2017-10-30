---
title: "預測 (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PREDICT
dev_langs:
- kbMDX
helpviewer_keywords:
- Predict function
ms.assetid: a82f3edd-249b-4559-98d3-6e10d81a095d
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 7bec1c96bd70b9b75c3a8c212cf1f6c04c27c73e
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="predict-mdx"></a>Predict (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

    
> [!CAUTION]  
>  這個函式位於由於內部不一致而移除的處理序中。  
>   
>  請檢閱＜範例＞一節中使用 DMX 運算式的解決方法。  
  
 傳回數值運算式在某個資料採擷模型上所評估出的值。  
  
## <a name="syntax"></a>語法  
  
```  
  
Predict(Mining_Model_Name,String_Expression)   
```  
  
## <a name="arguments"></a>引數  
 *Mining_Model_Name*  
 代表採礦模型名稱的有效字串運算式。  
  
 *String_Expression*  
 評估為指定採礦模型之有效 DMX 運算式的有效字串運算式。  
  
## <a name="remarks"></a>備註  
 **預測**函式會評估指定的採礦模型的內容中指定的字串運算式。  
  
 資料採礦語法及函數的相關文件，記錄於資料採礦運算式 (DMX) 參考中。  
  
## <a name="example"></a>範例  
 下列範例使用客戶群集採礦模型來預測群集名稱，以及特定客戶與群集的距離：  
  
```  
WITH MEMBER MEASURES.CLNAME AS   
PREDICT("Customer Clusters", "Cluster()")  
MEMBER MEASURES.CLDISTANCE AS   
PREDICT("Customer Clusters", "ClusterDistance(Cluster())")  
SELECT {MEASURES.CLNAME, MEASURES.CLDISTANCE} ON 0   
FROM [Adventure Works]  
WHERE([Customer].[Customer Geography].[Customer].&[12012])  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

