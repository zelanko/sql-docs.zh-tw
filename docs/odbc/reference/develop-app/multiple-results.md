---
title: 多個結果 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d90414b631a7e81a7868ab7974b64ea84a0ea452
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302407"
---
# <a name="multiple-results"></a>多個結果
*結果是*執行語句后數據源返回的內容。 ODBC 有兩種類型的結果:結果集和行計數。 *行計數*是受更新、刪除或插入語句影響的行數。 批次處理(在[SQL 語句的批次處理](../../../odbc/reference/develop-app/batches-of-sql-statements.md)中描述)可以生成多個結果。  
  
 下表列出了應用程式用於確定資料來源是否返回每種不同類型的批處理的多個結果的**SQLGetInfo**選項。 特別是,數據源可以為批處理中的每個語句返回整個語句的單個行計數或單個行計數。 對於使用參數陣列執行的結果集生成語句,資料源可以為每個參數集返回一個結果集或每個參數集的單個結果集。  
  
|批次類型|行計數|結果集|  
|----------------|----------------|-----------------|  
|明確批次處理|SQL_BATCH_ROW_COUNT[a]|--[b]|  
|程序|SQL_BATCH_ROW_COUNT[a]|--[b]|  
|參數陣列|SQL_PARAM_ARRAYS_ROW_COUNTS|SQL_PARAM_ARRAYS_SELECTS|  
  
 [a] 批處理中的行計數生成語句可能受支援,但不支援行計數的返回。 **SQLGetInfo**中的SQL_BATCH_SUPPORT選項指示是否允許批量生成行計數語句;因此,是否允許批量生成行計數語句。SQL_BATCH_ROW_COUNTS選項指示是否將這些行計數返回到應用程式。  
  
 [b] 顯式批處理和過程在包含多個結果集生成語句時始終返回多個結果集。  
  
> [!NOTE]  
>  ODBC 1.0 中引入的SQL_MULT_RESULT_SETS選項僅提供有關是否可以返回多個結果集的一般資訊。 特別是,如果返回SQL_BS_SELECT_EXPLICIT位或SQL_BS_SELECT_PROC位以SQL_BATCH_SUPPORT,或者返回SQL_PAS_BATCH以SQL_PARAM_ARRAYS_SELECT,則設置為"Y"。  
  
 要處理多個結果,應用程式呼叫**SQLMore 結果**。 此函數放棄當前結果,並使下一個結果可用。 當沒有更多結果可用時,它將返回SQL_NO_DATA。 例如,假設以下語句作為批次處理執行:  
  
```  
SELECT * FROM Parts WHERE Price > 100.00;  
UPDATE Parts SET Price = 0.9 * Price WHERE Price > 100.00  
```  
  
 執行這些語句後,應用程式將從**SELECT**語句創建的結果集中提取行。 提取行后,它將調用**SQLMore 結果**以提供重新定價的零件數。 如有必要 **,SQLMore結果**將丟棄未提取的行並關閉游標。 然後,應用程式調用**SQLRowCount**以確定**更新**語句重新定價了多少部件。  
  
 在任何結果可用之前是否執行整個批處理語句,都是特定於驅動程式的。 在某些實現中,情況就是這樣;在另一些操作中,調用**SQLMore 結果**會觸發批處理中下一個語句的執行。  
  
 如果批處理中的一個語句失敗 **,SQLMore 結果**將返回SQL_ERROR或SQL_SUCCESS_WITH_INFO。 如果當語句失敗時批處理中止,或者失敗語句是批處理中的最後一個語句 **,SQLMore結果**將返回SQL_ERROR。 如果當語句失敗且失敗語句不是批處理中的最後一個語句時批處理未中止 **,SQLMore 結果**將返回SQL_SUCCESS_WITH_INFO。 SQL_SUCCESS_WITH_INFO指示至少生成了一個結果集或計數,並且批處理未中止。
