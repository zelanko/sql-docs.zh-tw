---
title: 建置在 MDX 中的量值 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: f0347835-4983-4d26-acbb-6c8fae7992bd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7587e3304d1464beb7ef94cd7d3093982f394bcc
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66074592"
---
# <a name="building-measures-in-mdx"></a>在 MDX 中建立量值
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
 [CREATE MEMBER 陳述式 &#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-member)   
 [MDX 函數參考 &#40;MDX&#41;](/sql/mdx/mdx-function-reference-mdx)   
 [SELECT 陳述式 &#40;MDX&#41;](/sql/mdx/mdx-data-manipulation-select)  
  
  
