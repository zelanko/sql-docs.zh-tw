---
title: '? : (條件) (SSIS 運算式) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- conditional operator (?:)
- '?: (conditional operator)'
ms.assetid: d38e6890-7338-4ce0-a837-2dbb41823a37
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4d1713e75acf4ad8e76cfdf309ede46523690b4b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48197258"
---
# <a name="--conditional-ssis-expression"></a>? : (條件) (SSIS 運算式)
  依據布林運算式的評估傳回兩個運算式的其中一個。 如果布林運算式的評估結果為 TRUE，則會評估第一個運算式，且結果為運算式的結果。 如果布林運算式的評估結果為 FALSE，則會評估第二個運算式，且其結果為運算式的結果。  
  
## <a name="syntax"></a>語法  
  
```  
  
boolean_expression?expression1:expression2  
  
```  
  
## <a name="arguments"></a>引數  
 *boolean_expression*  
 評估為 TRUE、FALSE 或 NULL 的任何有效運算式。  
  
 *expression1*  
 任何有效的運算式。  
  
 *expression2*  
 任何有效的運算式。  
  
## <a name="result-types"></a>結果類型  
 *expression1* 或 *expression2*的資料類型。  
  
## <a name="remarks"></a>備註  
 如果 *boolean_expression* 評估為 NULL，則運算式結果為 NULL。 如果選取的運算式 ( *expression1* 或 *expression2* ) 為 NULL，則結果為 NULL。 如果選取的運算式不為 NULL，但未選取的運算式為 NULL，則結果為所選運算式的值。  
  
 如果 *expression1* 和 *expression2* 的資料類型相同，則結果即為該資料類型。 下列其他規則適用於結果類型：  
  
-   DT_TEXT 資料類型需要 *expression1* 和 *expression2* 擁有相同的字碼頁。  
  
-   DT_BYTES 資料類型的結果，其長度為較長引數的長度。  
  
 運算式組合 *expression1* 和 *expression2*必須評估為有效的資料類型並遵循下列其中一個規則：  
  
-   **數值** — *expression1* 與 *expression2* 都必須是數值資料類型。 資料類型的交集必須是運算式評估工具執行之隱含數值轉換規則中所指定的數值資料類型。 兩個數值資料類型的交集不能是 Null。 如需相關資訊，請參閱 [Integration Services Data Types in Expressions](integration-services-data-types-in-expressions.md)。  
  
-   **字串** *expression1* 和 *expression2* 都必須是字串資料類型：DT_STR 或 DT_WSTR。 兩個運算式可以評估為不同的字串資料類型。 結果的資料類型為 DT_WSTR，且長度為較長引數的長度。  
  
-   **日期、時間或日期/時間** ： *expression1* 和 *expression2* 都必須評估為下列其中一種資料類型：DT_DBDATE、DT_DATE、DT_DBTIME、DT_DBTIME2、DT_DBTIMESTAMP、DT_DBTIMESTAMP2、DT_DBTIMESTAPMOFFSET 或 DT_FILETIME。  
  
    > [!NOTE]  
    >  系統不支援評估為時間資料類型之運算式與評估為日期或日期/時間資料類型之運算式之間的比較。 系統會產生錯誤。  
  
     比較運算式時，系統會以列出的順序套用下列轉換規則：  
  
    -   當兩個運算式評估為相同的資料類型時，會擲行該資料類型的比較。  
  
    -   如果一個運算式為 DT_DBTIMESTAMPOFFSET 資料類型，另一個運算式會以隱含的方式轉換為 DT_DBTIMESTAMPOFFSET，而且會執行 DT_DBTIMESTAMPOFFSET 比較。 如需相關資訊，請參閱 [Integration Services Data Types in Expressions](integration-services-data-types-in-expressions.md)。  
  
    -   如果一個運算式為 DT_DBTIMESTAMP2 資料類型，另一個運算式會以隱含的方式轉換為 DT_DBTIMESTAMP2，而且會執行 DT_DBTIMESTAMP2 比較。  
  
    -   如果一個運算式為 DT_DBTIME2 資料類型，另一個運算式會以隱含的方式轉換為 DT_DBTIME2，而且會執行 DT_DBTIME2 比較。  
  
    -   如果一個運算式的類型不屬於 DT_DBTIMESTAMPOFFSET、DT_DBTIMESTAMP2 或 DT_DBTIME2，運算式會在進行比較前，轉換為 DT_DBTIMESTAMP 資料類型。  
  
     比較運算式時，系統會進行下列假設：  
  
    -   如果每個運算式都是包含毫秒的資料類型，系統會假設毫秒位數最少之資料類型的其餘位數為零。  
  
    -   如果每個運算式都是日期資料類型，但是只有一個運算式具有時區時差，則系統會假設沒有時區時差的日期資料類型為 Coordinated Universal Time (UTC)。  
  
 如需有關資料類型的詳細資訊，請參閱＜ [Integration Services Data Types](../data-flow/integration-services-data-types.md)＞。  
  
## <a name="expression-examples"></a>運算式範例  
 此範例顯示條件式地評估為 `savannah` 或 `unknown`的運算式。  
  
```  
@AnimalName == "Elephant"? "savannah": "unknown"  
```  
  
 此範例顯示參考 **ListPrice** 資料行的運算式。 **ListPrice** 的資料類型為 DT_CY。 此運算式會條件式地將 **ListPrice** 乘以 .2 或 .1。  
  
```  
ListPrice < 350.00 ? ListPrice * .2 : ListPrice * .1  
```  
  
## <a name="see-also"></a>另請參閱  
 [運算子優先順序和關聯性](operator-precedence-and-associativity.md)   
 [運算子&#40;SSIS 運算式&#41;](operators-ssis-expression.md)  
  
  
