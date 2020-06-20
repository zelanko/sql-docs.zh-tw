---
title: '- (負) (SSIS 運算式) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- '- (negative)'
- negative operator (-)
ms.assetid: f0118dfc-aced-4de2-953e-5ebf9c962b8d
author: janinezhang
ms.author: janinez
ms.openlocfilehash: ac803cb797644d47c6bc5ee4fcee99e14ba88a4c
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84969188"
---
# <a name="--negate-ssis-expression"></a>- (負) (SSIS 運算式)
  執行數值運算式的否定運算。  
  
## <a name="syntax"></a>語法  
  
```  
  
-numeric_expression  
  
```  
  
## <a name="arguments"></a>引數  
 *numeric_expression*  
 是任何數值資料類型的任何有效運算式。 只支援帶正負號的數值資料類型。 如需詳細資訊，請參閱 [Integration Services 資料類型](../data-flow/integration-services-data-types.md)。  
  
## <a name="result-types"></a>結果類型  
 傳回 *numeric_expression*的資料類型。  
  
## <a name="expression-examples"></a>運算式範例  
 此範例會執行 **Counter** 變數值的否定運算並與數值常值 50 相加。  
  
```  
-@Counter + 50  
```  
  
## <a name="see-also"></a>另請參閱  
 [運算子優先順序與關聯性](operator-precedence-and-associativity.md)   
 [運算子 &#40;SSIS 運算式&#41;](operators-ssis-expression.md)  
  
  
