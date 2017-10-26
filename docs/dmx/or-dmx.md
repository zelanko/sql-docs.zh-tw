---
title: "或者 (DMX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OR
dev_langs:
- DMX
helpviewer_keywords:
- OR operator
ms.assetid: 727a38a9-7f75-4963-8e8a-aa703c129d30
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 41cdd1638dc31eefa9cb034db33ef9d30162d617
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="or-dmx"></a>OR (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在兩個數值運算式上執行邏輯分離的邏輯運算子。  
  
## <a name="syntax"></a>語法  
  
```  
  
Expression1 OR Expression2  
```  
  
#### <a name="parameters"></a>參數  
 *Expression1*  
 有效的資料採礦延伸模組 (DMX) 運算式，會傳回數值。  
  
 *Expression2*  
 傳回數值的有效 DMX 運算式。  
  
## <a name="return-value"></a>傳回值  
 一個布林值，如果任一個引數或兩個引數都評估為 TRUE，就會傳回 TRUE；否則為 FALSE。  
  
## <a name="remarks"></a>備註  
 運算子執行邏輯分離之前，兩個引數都會當成布林值處理 (0 為 FALSE；否則為 TRUE)。 如果任一個引數或兩個引數都評估為 TRUE，則運算子會傳回 TRUE。 如果*Expression1*評估為 TRUE 和*Expression2*評估為 FALSE，則運算子會傳回 TRUE。  
  
 下表說明如何執行邏輯分離。  
  
|如果 Expression1 為|如果 Expression2 為|傳回值為|  
|-----------------------|-----------------------|---------------------|  
|TRUE|TRUE|TRUE|  
|TRUE|FALSE|TRUE|  
|FALSE|TRUE|TRUE|  
|FALSE|FALSE|FALSE|  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組 &#40; DMX &#41;運算子參考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [邏輯運算子 &#40; DMX &#41;](../dmx/operators-logical.md)   
 [運算子 &#40; DMX &#41;](../dmx/operators-dmx.md)  
  
  

