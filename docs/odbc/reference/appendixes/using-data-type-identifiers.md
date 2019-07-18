---
title: 使用資料型別識別項 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], identifiers
- identifiers [ODBC], data types
ms.assetid: 467e0c0c-a818-4737-8a24-3d8e15c7e162
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2b5e9fea64986bf595676540d74bb87a6e62521c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68070010"
---
# <a name="using-data-type-identifiers"></a>使用資料類型識別碼
應用程式會將資料型別識別項用於兩種方式： 來描述驅動程式，其緩衝區，以及擷取的結果集從驅動程式，好讓它們可以判斷要用來儲存資料緩衝處理的 C 類型相關的中繼資料。 應用程式呼叫下列函式，執行下列工作：  
  
-   **SQLBindParameter**， **SQLBindCol**，以及**SQLGetData** -來描述應用程式緩衝區的 C 資料類型。  
  
-   **SQLBindParameter** -來描述 SQL 資料類型的動態參數。  
  
-   **SQLColAttribute**並**SQLDescribeCol** -以擷取結果集資料行的 SQL 資料類型。  
  
-   **SQLDescribeParameter** -擷取 SQL 資料類型的參數。  
  
-   **SQLColumns**， **SQLProcedureColumns**，以及**SQLSpecialColumns** -擷取 SQL 資料類型的各種不同的結構描述資訊  
  
-   **SQLGetTypeInfo** -擷取一份支援的資料類型  
  
 資料型別識別項會儲存在 SQL_DESC_CONCISE_TYPE 欄位描述元。 描述元函式**SQLSetDescField**並**SQLSetDescRec**可以搭配適當的類型來執行上述清單中所列的工作。 如需詳細資訊，請參閱 < [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。
