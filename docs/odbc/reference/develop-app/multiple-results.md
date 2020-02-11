---
title: 多個結果 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLMoreResults function [ODBC], multiple results
- row counts [ODBC]
- multiple results [ODBC]
- result sets [ODBC], multiple results
- SQLGetInfo function [ODBC], multiple results
ms.assetid: a3c32e4b-8fe7-4a33-ae39-ae664001f315
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f8679bea49b63ffd5dc7164942b42ac9eed7e9ab
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68086358"
---
# <a name="multiple-results"></a>多個結果
*結果*是在執行語句之後，資料來源所傳回的內容。 ODBC 有兩種類型的結果：結果集和資料列計數。 資料*列計數*是由 update、delete 或 insert 語句所影響的資料列數目。 批次（ [SQL 語句的批次](../../../odbc/reference/develop-app/batches-of-sql-statements.md)中所述）可能會產生多個結果。  
  
 下表列出應用程式用來判斷資料來源是否會針對每個不同類型的批次傳回多個結果的**SQLGetInfo**選項。 特別是，資料來源可以針對批次中的每個語句，傳回整個語句批次或個別資料列計數的單一資料列計數。 在以參數陣列執行結果集產生語句的情況下，資料來源可以針對每一組參數，傳回所有參數集或個別結果集的單一結果集。  
  
|批次類型|資料列計數|結果集|  
|----------------|----------------|-----------------|  
|明確批次|SQL_BATCH_ROW_COUNT [a]|--[b]|  
|程序|SQL_BATCH_ROW_COUNT [a]|--[b]|  
|參數陣列|SQL_PARAM_ARRAYS_ROW_COUNTS|SQL_PARAM_ARRAYS_SELECTS|  
  
 [a] 可能會支援批次中的資料列計數產生語句，但不支援傳回資料列計數。 **SQLGetInfo**中的 SQL_BATCH_SUPPORT 選項會指出批次中是否允許資料列計數產生的語句;SQL_BATCH_ROW_COUNTS 選項會指出這些資料列計數是否會傳回給應用程式。  
  
 [b] 明確批次和套裝程式含多個結果集產生語句時，一律會傳回多個結果集。  
  
> [!NOTE]  
>  ODBC 1.0 中引進的 SQL_MULT_RESULT_SETS 選項，只提供有關是否可以傳回多個結果集的一般資訊。 特別是，如果為 SQL_BATCH_SUPPORT 傳回 SQL_BS_SELECT_EXPLICIT 或 SQL_BS_SELECT_PROC 位，或針對 SQL_PARAM_ARRAYS_SELECT 傳回 SQL_PAS_BATCH，則會設定為 "Y"。  
  
 若要處理多個結果，應用程式會呼叫**SQLMoreResults**。 此函式會捨棄目前的結果，並讓下一個結果可供使用。 當沒有其他可用的結果時，它會傳回 SQL_NO_DATA。 例如，假設下列語句是以批次方式執行：  
  
```  
SELECT * FROM Parts WHERE Price > 100.00;  
UPDATE Parts SET Price = 0.9 * Price WHERE Price > 100.00  
```  
  
 執行這些語句之後，應用程式會從**SELECT**語句所建立的結果集提取資料列。 完成提取資料列時，它會呼叫**SQLMoreResults** ，以提供已 repriced 的部分數目。 如有必要， **SQLMoreResults**會捨棄 unfetched 的資料列，並關閉資料指標。 然後，應用程式會呼叫**SQLRowCount**來判斷**UPDATE**語句 repriced 多少部分。  
  
 無論是否在有任何結果可用之前執行整個批次語句，都是驅動程式特有的。 在某些情況下，這種情況如下：在其他情況下，呼叫**SQLMoreResults**會觸發批次中下一個語句的執行。  
  
 如果批次中的其中一個語句失敗， **SQLMoreResults**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO。 如果批次在語句失敗或失敗的語句是批次中的最後一個語句時中止，則**SQLMoreResults**會傳回 SQL_ERROR。 如果當語句失敗且 failed 語句不是批次中的最後一個語句時，批次未中止，則**SQLMoreResults**會傳回 SQL_SUCCESS_WITH_INFO。 SQL_SUCCESS_WITH_INFO 表示至少產生一個結果集或計數，而且批次未中止。
