---
title: "父子式維度中的自訂積存運算子 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- child rollup operations
- UnaryOperatorColumn property
- custom rollup operators [Analysis Services]
- unary operators
- parent-child dimensions [Analysis Services]
ms.assetid: a3ddd9fc-5fa3-4227-9322-8c45a5b5c2c3
caps.latest.revision: "26"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 84ed7fd34e017fe0ea076822d1931ea1143b5849
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="parent-child-dimension-attributes---custom-rollup-operators"></a>父子式維度屬性自訂積存運算子
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]自訂積存運算子提供簡易的方法，控制成員值到父系值中的父子式階層中的積存方式。 在包含父子式關聯性的維度中，您可指定包含一元運算子的資料行，為父屬性的所有非導出成員指定積存。 只要評估父成員的值時，就會將一元運算子套用至成員。  
  
 儲存一元運算子的資料行是由父屬性之 **UnaryOperatorColumn** 屬性定義的，並會套用到屬性的每個成員。 此屬性指定的資料行可位於維度資料表中，或依維度資料表中的外部索引鍵，位於與維度資料表有關的資料表中。  
  
 自訂積存運算子提供的功能與自訂成員公式類似，但較為簡化。 自訂成員公式使用多維度運算式 (MDX) 運算式來決定如何積存成員。 相反地，自訂積存運算子使用簡單的一元運算子來決定成員的值如何影響父系。 在維度中，前一個層級的自訂成員公式會覆寫層級的自訂積存運算子。  
  
## <a name="custom-rollup-precedence"></a>自訂積存優先順序  
 在優先順序方面，階層中某個層級之來源屬性的自訂積存運算子，會覆寫前一個層級的自訂成員公式。 然而，先前層級的自訂成員公式會覆寫一層級的自訂積存運算子。  
  
## <a name="see-also"></a>請參閱  
 [定義自訂成員公式](../../analysis-services/multidimensional-models/attribute-properties-define-custom-member-formulas.md)   
 [父子式維度中的一元運算子](../../analysis-services/multidimensional-models/parent-child-dimension-attributes-unary-operators.md)  
  
  
