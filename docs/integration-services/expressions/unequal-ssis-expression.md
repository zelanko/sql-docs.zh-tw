---
title: '!= (不等於) (SSIS 運算式) | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- unequal operator (!=)
- '!= (not equal to)'
ms.assetid: fad20e85-c0e6-42bf-af70-2bc80ee09be5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f8f00f51ee6db4b93ba56211755e067c008898c4
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/20/2019
ms.locfileid: "58271393"
---
# <a name="-unequal-ssis-expression"></a>!= (不等於) (SSIS 運算式)
  執行比較來決定兩個資料類型相容的運算式是否不相等。 運算式評估工具會在執行比較之前，自動轉換許多資料類型。  
  
 但是，某些資料類型要求運算式先包含明確轉換，才能成功評估運算式。 如需在資料類型間合法轉換的詳細資訊，請參閱[轉換 &#40;SSIS 運算式&#41;](../../integration-services/expressions/cast-ssis-expression.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
expression1 != expression2  
  
```  
  
## <a name="arguments"></a>引數  
 *expression1, expression2*  
 任何有效的運算式。  
  
## <a name="result-types"></a>結果類型  
 DT_BOOL  
  
## <a name="remarks"></a>Remarks  
 如果比較中的任一個運算式為 Null，則比較結果為 Null。 如果兩個運算式都是 Null，結果則為 Null。  
  
 運算式集 *expression1* 與 *expression2*必須遵循下列規則之一：  
  
-   **數值** — *expression1* 與 *expression2* 都必須是數值資料類型。 資料類型的交集必須是運算式評估工具執行之隱含數值轉換規則中所指定的數值資料類型。 兩個數值資料類型的交集不能是 Null。 如需相關資訊，請參閱 [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md)。  
  
-   **字元** ： *expression1* 和 *expression2* 都必須評估為 DT_STR 或 DT_WSTR 資料類型。 兩個運算式可以評估為不同的字串資料類型。  
  
    > [!NOTE]  
    >  字串比較有區分大小寫、腔調字、假名與全半形。  
  
-   **日期、時間或日期/時間** *expression1* 和 *expression2* 都必須評估為下列其中一個資料類型：DT_DBDATE、DT_DATE、DT_DBTIME、DT_DBTIME2、DT_DBTIMESTAMP、DT_DBTIMESTAMP2、DT_DBTIMESTAPMOFFSET 或 DT_FILETIME。  
  
    > [!NOTE]  
    >  系統不支援評估為時間資料類型之運算式與評估為日期或日期/時間資料類型之運算式之間的比較。 系統會產生錯誤。  
  
     比較運算式時，系統會以列出的順序套用下列轉換規則：  
  
    -   當兩個運算式評估為相同的資料類型時，會擲行該資料類型的比較。  
  
    -   如果一個運算式為 DT_DBTIMESTAMPOFFSET 資料類型，另一個運算式會以隱含的方式轉換為 DT_DBTIMESTAMPOFFSET，而且會執行 DT_DBTIMESTAMPOFFSET 比較。 如需相關資訊，請參閱 [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md)。  
  
    -   如果一個運算式為 DT_DBTIMESTAMP2 資料類型，另一個運算式會以隱含的方式轉換為 DT_DBTIMESTAMP2，而且會執行 DT_DBTIMESTAMP2 比較。  
  
    -   如果一個運算式為 DT_DBTIME2 資料類型，另一個運算式會以隱含的方式轉換為 DT_DBTIME2，而且會執行 DT_DBTIME2 比較。  
  
    -   如果一個運算式的類型不屬於 DT_DBTIMESTAMPOFFSET、DT_DBTIMESTAMP2 或 DT_DBTIME2，運算式會在進行比較前，轉換為 DT_DBTIMESTAMP 資料類型。  
  
     比較運算式時，系統會進行下列假設：  
  
    -   如果每個運算式都是包含毫秒的資料類型，系統會假設毫秒位數最少之資料類型的其餘位數為零。  
  
    -   如果每個運算式都是日期資料類型，但是只有一個運算式具有時區時差，則系統會假設沒有時區時差的日期資料類型為 Coordinated Universal Time (UTC)。  
  
-   **邏輯** — *expression1* 與 *expression2* 都必須評估為布林。  
  
-   **GUID** ： *expression1* 和 *expression2* 都必須評估為 DT_GUID 資料類型。  
  
-   **二進位** ： *expression1* 和 *expression2* 都必須評估為 DT_BYTES 資料類型。  
  
-   **BLOB** *expression1* 和 *expression2* 都必須評估為相同的二進位大型物件區塊 (BLOB) 資料類型：DT_TEXT、DT_NTEXT 或 DT_IMAGE。  
  
 如需有關資料類型的詳細資訊，請參閱＜ [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)＞。  
  
## <a name="expression-examples"></a>運算式範例  
 只有在目前日期不是 2003 年 7 月 4 日時，此範例的評估結果才會是 TRUE。 如需詳細資訊，請參閱 [GETDATE &#40;SSIS 運算式&#41;](../../integration-services/expressions/getdate-ssis-expression.md)。  
  
```  
"7/4/2003" != GETDATE()  
```  
  
 如果 **ListPrice** 資料行中的值不是 500，則此範例評估結果為 TRUE。  
  
```  
ListPrice != 500  
```  
  
 這個範例使用變數 **LPrice**。 如果 **LPrice** 的值不是 500，則其評估結果為 TRUE。 變數的資料類型必須是數值，運算式才能進行剖析。  
  
```  
@LPrice != 500  
```  
  
## <a name="see-also"></a>另請參閱  
 [== &#40;等於&#41; &#40;SSIS 運算式&#41;](../../integration-services/expressions/equal-ssis-expression.md)   
 [運算子優先順序與關聯性](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [運算子 &#40;SSIS 運算式&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
