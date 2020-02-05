---
title: REVERSE (SSIS 運算式) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- REVERSE function
- reverse character expressions
ms.assetid: bcebcc55-7247-4896-8f53-4d582d58cfb4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d7a0e8974f781f5f69817cf3374416de7bc32580
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "71288380"
---
# <a name="reverse-ssis-expression"></a>REVERSE (SSIS 運算式)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


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
  
## <a name="see-also"></a>另請參閱  
 [函數 &#40;SSIS 運算式&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
