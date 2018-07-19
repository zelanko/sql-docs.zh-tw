---
title: 多個結果 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLMoreResults function [ODBC], multiple results
- row counts [ODBC]
- multiple results [ODBC]
- result sets [ODBC], multiple results
- SQLGetInfo function [ODBC], multiple results
ms.assetid: a3c32e4b-8fe7-4a33-ae39-ae664001f315
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: be6cb4a2f7f03e63e3da9345b833b0382edd8e9d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32913843"
---
# <a name="multiple-results"></a>多個結果
A*結果*項目之後，傳回資料來源所執行的陳述式。 ODBC 有兩種類型的結果： 結果集和資料列計數。 *資料列計數*會更新，受影響資料列數目 delete 或 insert 陳述式。 批次中所述[批次的 SQL 陳述式](../../../odbc/reference/develop-app/batches-of-sql-statements.md)，可以產生多個結果。  
  
 下表列出**SQLGetInfo**應用程式可用來判斷資料來源是否傳回各種不同類型的批次的多個結果的選項。 特別是，資料來源可以傳回單一資料列計數，整個批次的陳述式或批次中每個陳述式的個別資料列計數。 如果結果集產生 – 執行陳述式參數的陣列，是資料來源可以傳回單一結果集，所有的參數集或個別的結果設定每個參數集。  
  
|批次類型|資料列計數|結果集|  
|----------------|----------------|-----------------|  
|明確的批次|SQL_BATCH_ROW_COUNT [a]|-[b]。|  
|程序|SQL_BATCH_ROW_COUNT [a]|-[b]。|  
|參數陣列|SQL_PARAM_ARRAYS_ROW_COUNTS|SQL_PARAM_ARRAYS_SELECTS|  
  
 不支援 [a] 資料列計數 – 產生批次中的陳述式可能會受到支援，但傳回的資料列計數。 中的 SQL_BATCH_SUPPORT 選項**SQLGetInfo**指出是否資料列計數-產生的陳述式批次中宣告; SQL_BATCH_ROW_COUNTS 選項指出應用程式是否會傳回這些資料列計數。  
  
 [b] 明確的批次和程序一律傳回多個結果集，包含多個結果集 – 產生陳述式時。  
  
> [!NOTE]  
>  ODBC 1.0 中導入 SQL_MULT_RESULT_SETS 選項提供有關是否可以傳回多個結果集只一般資訊。 特別是，它設定為"Y"如果 SQL_BS_SELECT_EXPLICIT 或 SQL_BS_SELECT_PROC 位元會傳回 SQL_BATCH_SUPPORT 或 SQL_PAS_BATCH SQL_PARAM_ARRAYS_SELECT 都會傳回。  
  
 若要處理多個結果，應用程式呼叫**SQLMoreResults**。 此函式會捨棄目前的結果，並提供下一個結果。 當沒有其他結果可用時，它會傳回 sql_no_data 為止。 例如，假設下列陳述式會以批次執行：  
  
```  
SELECT * FROM Parts WHERE Price > 100.00;  
UPDATE Parts SET Price = 0.9 * Price WHERE Price > 100.00  
```  
  
 應用程式執行這些陳述式之後，會從所建立的結果集提取資料列**選取**陳述式。 完成提取資料列時，它會呼叫**SQLMoreResults**將提供了 repriced 的部分數目。 如有必要， **SQLMoreResults**會捨棄未提取的資料列，並關閉資料指標。 接著，應用程式呼叫**SQLRowCount**來判斷多少部分由 repriced**更新**陳述式。  
  
 它是特定驅動程式是否整個批次陳述式才可供任何結果。 在某些實作中，是這種情況。在其他呼叫**SQLMoreResults**觸發批次中的下一個陳述式執行。  
  
 如果其中一個批次中陳述式失敗， **SQLMoreResults**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO。 如果陳述式失敗，或失敗的陳述式是批次中的最後一個陳述式時，批次已中止**SQLMoreResults**將會傳回 SQL_ERROR。 如果陳述式失敗後失敗的陳述式不是批次中的最後一個陳述式批次未中止**SQLMoreResults**將會傳回 SQL_SUCCESS_WITH_INFO。 SQL_SUCCESS_WITH_INFO，表示已產生至少一個結果集或計數，而且未中止批次。
