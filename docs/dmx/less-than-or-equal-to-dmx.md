---
title: "&lt;= （小於或等於） (DMX) |Microsoft 文件"
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
dev_langs:
- DMX
helpviewer_keywords:
- <= (less than or equal to operator)
- less than or equal to operator (<=)
ms.assetid: 4f7135e8-1e27-4568-a9df-668454b4cdde
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 90cdc1157ca7918da48547bdac4c2e3146458d60
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="lt-less-than-or-equal-to-dmx"></a>&lt;= （小於或等於） (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  執行比較作業，判斷某個資料採礦延伸模組 (DMX) 運算式的值是否小於或等於另一個 DMX 運算式的值。  
  
## <a name="syntax"></a>語法  
  
```  
  
DMX_Expression <= DMX_Expression  
```  
  
#### <a name="parameters"></a>參數  
 *DMX_Expression*  
 有效的 DMX 運算式。  
  
## <a name="return-value"></a>傳回值  
 一個布林值，其中如果兩個參數都為非 Null，而且第一個參數的值小於或等於第二個參數的值，則為 TRUE。 如果兩個參數都為非 Null，而且第一個參數的值大於第二個參數的值，則布林值為 FALSE。 如果任一個參數或兩個參數都評估為 Null 值，則布林值為 Null 值。  
  
## <a name="see-also"></a>另請參閱  
 [比較運算子 &#40; DMX &#41;](../dmx/operators-comparison.md)   
 [資料採礦延伸模組 &#40; DMX &#41;運算子參考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [運算子 &#40; DMX &#41;](../dmx/operators-dmx.md)  
  
  

