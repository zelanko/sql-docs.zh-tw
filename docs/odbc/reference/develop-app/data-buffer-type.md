---
title: 資料緩衝區類型 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 615625ca396e5f2ae094962457cc9e746730ddcf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68067408"
---
# <a name="data-buffer-type"></a>資料緩衝區類型
緩衝區的 C 資料類型是由應用程式所指定。 使用單一變數時，當應用程式佈建變數時，就會發生這種情況。 使用泛型記憶體時（也就是，類型為 void 的指標所指向的記憶體），會在應用程式將記憶體轉換成特定類型時發生。 驅動程式會以兩種方式探索此類型：  
  
-   **資料緩衝區類型引數。** 用來傳送參數值和結果集資料的緩衝區（例如，在**SQLBindCol**中與*TargetValuePtr*系結的緩衝區）通常會有相關聯的類型引數，例如**SQLBindCol**中的*TargetType*引數。 在這個引數中，應用程式會傳遞對應至緩衝區類型的 C 類型識別碼。 例如，在下列對**SQLBindCol**的呼叫中，值 SQL_C_TYPE_DATE 會告訴驅動程式該*日期*緩衝區為 SQL_DATE_STRUCT：  
  
    ```  
    SQL_DATE_STRUCT Date;  
    SQLINTEGER  DateInd;  
    SQLBindCol(hstmt, 1, SQL_C_TYPE_DATE, &Date, 0, &DateInd);  
    ```  
  
     如需類型識別碼的詳細資訊，請參閱本節稍後的[ODBC 中的資料類型](../../../odbc/reference/develop-app/data-types-in-odbc.md)一節。  
  
-   **預先定義的類型。** 用來傳送和抓取選項或屬性的緩衝區（例如**SQLGetInfo**中的*InfoValuePtr*引數所指向的緩衝區）具有根據指定選項而定的固定類型。 驅動程式會假設資料緩衝區屬於這種類型;應用程式必須負責配置此類型的緩衝區。 例如，在下列對**SQLGetInfo**的呼叫中，驅動程式會假設緩衝區是32位整數，因為這是 SQL_STRING_FUNCTIONS 選項所需的：  
  
    ```  
    SQLUINTEGER StringFuncs;  
    SQLGetInfo(hdbc, SQL_STRING_FUNCTIONS, (SQLPOINTER) &StringFuncs, 0,  
                NULL);  
    ```  
  
 驅動程式會使用 C 資料類型來解讀緩衝區中的資料。
