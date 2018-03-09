---
title: "建置在 MDX 中的量值 |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f0347835-4983-4d26-acbb-6c8fae7992bd
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d7c10b66d6ba27d406c2682b2aea3b8858c8fd12
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2018
---
# <a name="mdx-building-measures"></a>MDX 建立量值
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
在多維度運算式 (MDX) 中，量值是具名 DAX 運算式，藉由計算運算式以傳回表格式模型中的值而解析出來。 此一定義涵蓋的範圍相當廣泛。 在 MDX 查詢中建構和使用量值的能力，提供了許多管理表格式資料的功能。  
  
> [!WARNING]  
>  量值只能在表格式模型中定義；如果您的資料庫設定為多維度模式，建立量值將會產生錯誤。  
  
 若要建立定義為 MDX 查詢一部分的量值 (因此其範圍限制在查詢內)，請使用 WITH 關鍵字。 然後您就可以在 MDX SELECT 陳述式內使用量值。 使用這種方式，可以變更利用 WITH 關鍵字建立的導出成員，而不會影響到 SELECT 陳述式。 然而，在 MDX 中參考量值的方式不同於 DAX 運算式；若要參考量值，您要將它命名為 [Measures] 維度的成員，請參閱下列 MDX 範例：  
  
```  
with measure  'Sales Territory'[Total Sales Amount] = SUM('Internet Sales'[Sales Amount]) + SUM('Reseller Sales'[Sales Amount])  
select measures.[Total Sales Amount] on columns  
     ,NON EMPTY [Date].[Calendar Year].children on rows  
from [Model]  
  
```  
  
 執行時，它會傳回下列資料：  
  
||Total Sales Amount||  
|-|------------------------|-|  
|2001|11331808.96||  
|2002|30674773.18||  
|2003|41993729.72||  
|2004|25808962.34||  
  
## <a name="see-also"></a>另請參閱  
 [建立 MEMBER 陳述式 &#40;MDX &#41;](../../../mdx/mdx-data-definition-create-member.md)   
 [MDX 函數參考 &#40;MDX &#41;](../../../mdx/mdx-function-reference-mdx.md)   
 [SELECT 陳述式 &#40;MDX &#41;](../../../mdx/mdx-data-manipulation-select.md)  
  
  
