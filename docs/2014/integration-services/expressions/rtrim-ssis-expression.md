---
title: RTRIM (SSIS 運算式) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- RTRIM function
- trailing blanks
ms.assetid: 529bd43e-3f8a-4682-a33e-569176aa7fc4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 53d9bfbb7418a3bc6727ccc7160a5364bac39f58
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62768774"
---
# <a name="rtrim-ssis-expression"></a>RTRIM (SSIS 運算式)
  傳回移除尾端空白之後的字元運算式。  
  
> [!NOTE]  
>  RTRIM 不會移除空白字元，例如 Tab 鍵或換行字元。 Unicode 會為許多不同類型的空格提供字碼指標，但此功能只會辨識 Unicode 字碼指標 0x0020。 當將雙位元組字集 (DBCS) 字串轉換為 Unicode 時，它們可以包括 0x0020 以外的空格字元，但此功能無法移除這些空格。 若要移除所有種類的空格，您可以在從「指令碼」元件執行的指令碼中使用 Microsoft Visual Basic .NET RTrim 方法。  
  
## <a name="syntax"></a>語法  
  
```  
  
RTRIM(character expression)  
```  
  
## <a name="arguments"></a>引數  
 *character_expression*  
 要移除空白的字元運算式。  
  
## <a name="result-types"></a>結果類型  
 DT_WSTR  
  
## <a name="remarks"></a>備註  
 RTRIM 只適用於 DT_WSTR 資料類型。 如果 *character_expression* 引數是字串常值或具有 DT_STR 資料類型的資料行，則該引數會在 RTRIM 執行其作業前隱含轉換成 DT_WSTR 資料類型。 其他資料類型必須明確地轉換為 DT_WSTR 資料類型。 如需詳細資訊，請參閱 [Integration Services 資料類型](../data-flow/integration-services-data-types.md)和[轉換 &#40;SSIS 運算式&#41;](cast-ssis-expression.md)。  
  
 如果引數為 Null，則 RTRIM 會傳回 Null 結果。  
  
## <a name="expression-examples"></a>運算式範例  
 此範例會移除字串常值尾端的空白。 傳回結果為「Hello」。  
  
```  
RTRIM("Hello   ")  
```  
  
 此範例會移除 **FirstName** 和 **LastName** 資料行串連尾端的空白。  
  
```  
RTRIM(FirstName + " " + LastName)  
```  
  
 此範例會移除 **FirstName** 變數尾端的空白。  
  
```  
RTRIM(@FirstName)  
```  
  
## <a name="see-also"></a>另請參閱  
 [LTRIM &#40;SSIS 運算式&#41;](trim-ssis-expression.md)   
 [TRIM &#40;SSIS 運算式&#41;](trim-ssis-expression.md)   
 [函數 &#40;SSIS 運算式&#41;](functions-ssis-expression.md)  
  
  
