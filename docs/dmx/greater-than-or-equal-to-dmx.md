---
title: "&gt;= (大於或等於) (DMX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: DMX
helpviewer_keywords:
- '>= (greater than or equal to operator)'
- greater than or equal to (>=)
ms.assetid: a96b7e9c-72dc-4df1-aa41-85aad933df96
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: da7383aecf422f9ebdf43fe6932610423f3a34a9
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="gt-greater-than-or-equal-to-dmx"></a>&gt;= (大於或等於) (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  執行比較作業，判斷某個資料採礦延伸模組 (DMX) 運算式的值是否大於或等於另一個 DMX 運算式的值。  
  
## <a name="syntax"></a>語法  
  
```  
  
DMX_Expression >= DMX_Expression  
```  
  
#### <a name="parameters"></a>參數  
 *DMX_Expression*  
 有效的 DMX 運算式。  
  
## <a name="return-value"></a>傳回值  
 一個布林值，其中如果兩個參數都為非 Null，而且第一個參數的值大於或等於第二個參數的值，則為 TRUE。 如果兩個參數都為非 Null，而且第一個參數的值小於第二個參數的值，則布林值為 FALSE。 如果任一個參數或兩個參數都評估為 Null 值，則布林值為 Null 值。  
  
## <a name="see-also"></a>請參閱  
 [比較運算子 &#40; DMX &#41;](../dmx/operators-comparison.md)   
 [資料採礦延伸模組 &#40; DMX &#41;運算子參考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [運算子 &#40; DMX &#41;](../dmx/operators-dmx.md)  
  
  
