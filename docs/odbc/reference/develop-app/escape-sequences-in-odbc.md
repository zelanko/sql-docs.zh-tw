---
title: ODBC 中的逸出序列 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC]
- SQL statements [ODBC], escape sequences
- escape sequences [ODBC], about escape sequences
ms.assetid: cf229f21-6c38-4b5b-aca8-f1be0dfeb3d0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4d41b0c03ecbe6de63cba1a28a1f39f12a42dc86
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300418"
---
# <a name="escape-sequences-in-odbc"></a>ODBC 中的逸出序列
Dbms 通常會執行一些語言功能，例如外部聯結和純量函式呼叫。 不過，這些功能的語法傾向于 DBMS 專屬，即使標準語法是由各種標準本文所定義。 因此，ODBC 會定義包含下列語言功能之標準語法的 escape 序列：  
  
-   日期、時間、時間戳記和日期時間間隔常值  
  
-   純量函數，例如數值、字串和資料類型轉換函數  
  
-   LIKE 述詞 escape 字元  
  
-   外部聯結  
  
-   程序呼叫  
  
 ODBC 所使用的轉義順序如下所示：  
  
```  
  
(extension)  
  
```  
  
## <a name="remarks"></a>備註  
 逸出序列是由驅動程式辨識和剖析，這會以 DBMS 特定的文法取代逸出序列。 如需有關轉義順序語法的詳細資訊，請參閱附錄 C： SQL 文法中的[ODBC Escape 序列](../../../odbc/reference/appendixes/odbc-escape-sequences.md)。  
  
> [!NOTE]  
>  在 ODBC 2 中。*x*，這是逸出序列的標準語法： **--\*（廠商（**_廠商名稱_**），產品（**_產品名稱_**）**_延伸_ ** \*模組）--**  
>   
>  除了此語法之外，也定義了格式為 **{**_extension_**}** 的速記語法。  
>   
>  在 ODBC 3 中。*x*，逸出序列的長格式已被取代，而且會以獨佔方式使用速記格式。  
  
 由於逸出序列是由驅動程式對應到 DBMS 特定的語法，因此應用程式可以使用 escape 序列或 DBMS 特定的語法。 不過，使用 DBMS 特定語法的應用程式將無法互通。 使用 escape 序列時，應用程式應該確定已關閉 SQL_ATTR_NOSCAN 語句屬性，這是預設值。 否則，會將 escape 序列直接傳送至資料來源，通常會導致語法錯誤。  
  
 驅動程式只支援可對應至基礎語言功能的逸出序列。 例如，如果資料來源不支援外部聯結，驅動程式也不會。 為了判斷支援哪些 escape 序列，應用程式會呼叫**SQLGetTypeInfo**和**SQLGetInfo**。 如需詳細資訊，請參閱下一節、[日期、時間和時間戳記常](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)值。  
  
 此章節包含下列主題。  
  
-   [日期、時間和時間戳記常值](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)  
  
-   [純量函式呼叫](../../../odbc/reference/develop-app/scalar-function-calls.md)  
  
-   [LIKE 述詞逸出字元](../../../odbc/reference/develop-app/like-predicate-escape-character.md)  
  
-   [外部聯結](../../../odbc/reference/develop-app/outer-joins.md)  
  
-   [程序呼叫](../../../odbc/reference/develop-app/procedure-calls.md)
