---
title: 資料緩衝區類型 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], buffers
- data buffers [ODBC], types
- buffers [ODBC], data
- C data types [ODBC], buffers
ms.assetid: 58bea3e9-d552-447f-b3ad-ce1dab213b72
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9b98ed2ab0865b98884f6dfa1ff20142540ff314
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305244"
---
# <a name="data-buffer-type"></a>資料緩衝區類型
緩衝區的 C 數據類型由應用程式指定。 使用單個變數時,當應用程式分配變數時,將發生這種情況。 對於泛型記憶體(即由類型 void 指標指向的記憶體),當應用程式將記憶體轉換為特定類型時,就會發生這種情況。 驅動程式透過兩種方式發現此類型:  
  
-   **數據緩衝區類型參數。** 用於傳輸參數值和結果集數據的緩衝區(如**SQLBindCol**中與*TargetValuePtr*綁定的緩衝區)通常具有關聯的類型參數,如**SQLBindCol**中的*TargetType*參數。 在此參數中,應用程式傳遞對應於緩衝區類型的 C 類型識別碼。 例如,在以下對**SQLBindCol**的呼叫中,值SQL_C_TYPE_DATE告訴驅動程式*Date*緩衝區是SQL_DATE_STRUCT:  
  
    ```  
    SQL_DATE_STRUCT Date;  
    SQLINTEGER  DateInd;  
    SQLBindCol(hstmt, 1, SQL_C_TYPE_DATE, &Date, 0, &DateInd);  
    ```  
  
     有關類型識別碼的詳細資訊,請參閱本節後面的[ODBC 部分中的資料類型](../../../odbc/reference/develop-app/data-types-in-odbc.md)。  
  
-   **預定義類型。** 用於發送和檢索選項或屬性的緩衝區(如**SQLGetInfo**中*InfoValuePtr*參數指向的緩衝區)具有依賴於指定選項的固定類型。 驅動程式假定數據緩衝區是此類型;因此,驅動程式假定數據緩衝區為此類型。應用程式負責分配此類型的緩衝區。 例如,在以下對**SQLGetInfo**的呼叫中,驅動程式假定緩衝區是 32 位元整數,因為這是SQL_STRING_FUNCTIONS選項要求:  
  
    ```  
    SQLUINTEGER StringFuncs;  
    SQLGetInfo(hdbc, SQL_STRING_FUNCTIONS, (SQLPOINTER) &StringFuncs, 0,  
                NULL);  
    ```  
  
 驅動程式使用 C 數據類型來解釋緩衝區中的數據。
