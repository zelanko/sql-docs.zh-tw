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
manager: craigg
ms.openlocfilehash: 47e1250a92b78aefdc1611fd88e0ee9b0f772ad0
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52539905"
---
# <a name="multiple-results"></a>多個結果
A*結果*項目所傳回的資料來源之後執行的陳述式。 ODBC 有兩種類型的結果： 結果集和資料列計數。 *資料列計數*所刪除的更新時，受影響的資料列數目，或 insert 陳述式。 批次中所述[批次的 SQL 陳述式](../../../odbc/reference/develop-app/batches-of-sql-statements.md)，可以產生多個結果。  
  
 下表列出**SQLGetInfo**應用程式使用，以判斷資料來源是否傳回批次的每個不同類型的多個結果的選項。 特別是，資料來源可以傳回整個批次陳述式的單一資料列計數，或個別的資料列計數的批次中的每個陳述式。 如果結果集產生執行陳述式的參數陣列，是資料來源可以傳回單一結果集，使所有的參數集，或每個參數集的個別結果集。  
  
|批次類型|資料列計數|結果集|  
|----------------|----------------|-----------------|  
|明確的批次|[A] SQL_BATCH_ROW_COUNT|-[b]。|  
|程序|[A] SQL_BATCH_ROW_COUNT|-[b]。|  
|參數陣列|SQL_PARAM_ARRAYS_ROW_COUNTS|SQL_PARAM_ARRAYS_SELECTS|  
  
 不支援產生計數的批次中的陳述式可能會受到支援，[a] 資料列，但傳回的資料列計數。 中的 SQL_BATCH_SUPPORT 選項**SQLGetInfo**指出是否資料列計數產生允許陳述式批次; SQL_BATCH_ROW_COUNTS 選項可讓您指出應用程式是否會傳回這些資料列計數。  
  
 [b] 明確的批次和程序一律傳回多個結果集，包含多個結果集產生陳述式時。  
  
> [!NOTE]  
>  ODBC 1.0 中導入 SQL_MULT_RESULT_SETS 選項提供有關是否可以傳回多個結果集只一般資訊。 特別的是，它是設定為"Y"SQL_BS_SELECT_EXPLICIT 或 SQL_BS_SELECT_PROC 個位元會傳回 SQL_BATCH_SUPPORT 則 SQL_PAS_BATCH SQL_PARAM_ARRAYS_SELECT 會傳回。  
  
 若要處理多個結果，應用程式會呼叫**SQLMoreResults**。 此函式會捨棄目前的結果，並提供下一個結果。 沒有其他結果可用時，它會傳回 sql_no_data 為止。 例如，假設下列陳述式會以批次執行：  
  
```  
SELECT * FROM Parts WHERE Price > 100.00;  
UPDATE Parts SET Price = 0.9 * Price WHERE Price > 100.00  
```  
  
 應用程式會執行這些陳述式之後，會從所建立的結果集提取資料列**選取**陳述式。 完成擷取資料列時，它會呼叫**SQLMoreResults**提供已 repriced 的部分數目。 如果有必要，請**SQLMoreResults**會捨棄未提取的資料列，並關閉資料指標。 接著，應用程式會呼叫**SQLRowCount**來判斷多少部分由 repriced**更新**陳述式。  
  
 它是驅動程式特定的整個批次陳述式會有可用的任何結果之前執行。 在某些實作中，這會是大小寫，在其他呼叫**SQLMoreResults**觸發的批次中的下一個陳述式。  
  
 如果其中一個批次中陳述式失敗， **SQLMoreResults**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO。 如果陳述式失敗，或失敗的陳述式是批次中的最後一個陳述式時，批次已中止**SQLMoreResults**將會傳回 SQL_ERROR。 如果陳述式失敗和失敗的陳述式不是批次中的最後一個陳述式時未中止批次**SQLMoreResults**將會傳回 SQL_SUCCESS_WITH_INFO。 SQL_SUCCESS_WITH_INFO，表示至少一個結果集或計數，已產生，而且未中止批次。
