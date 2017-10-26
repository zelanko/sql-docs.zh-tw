---
title: "REVERSE （SSIS 運算式） |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- REVERSE function
- reverse character expressions
ms.assetid: bcebcc55-7247-4896-8f53-4d582d58cfb4
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: bb7529a91258c78d9bc8c752c775a5544975e7d0
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="reverse-ssis-expression"></a>REVERSE (SSIS 運算式)
  傳回反向順序的字元運算式。  
  
## <a name="syntax"></a>語法  
  
```  
  
REVERSE(character_expression)  
```  
  
## <a name="arguments"></a>引數  
 *character_expression*  
 是要反向的字元運算式。  
  
## <a name="result-types"></a>結果類型  
 DT_WSTR  
  
## <a name="remarks"></a>備註  
 *character_expression* 引數必須是 DT_WSTR 資料類型。  
  
 如果 *character_expression* 為 Null，則 REVERSE 會傳回 Null 結果。  
  
## <a name="expression-examples"></a>運算式範例  
 這個範例使用字串常值。 傳回結果為「ekiB niatnuoM」。  
  
```  
REVERSE("Mountain Bike")  
```  
  
 這個範例使用變數。 如果 **Name** 包含 Touring Bike，則傳回結果為 "ekiB gniruoT"。  
  
```  
REVERSE(@Name)  
```  
  
## <a name="see-also"></a>請參閱＜  
 [函式 &#40;SSIS 運算式 &#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  

