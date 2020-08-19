---
description: ODBC 中的逸出序列
title: ODBC 中的 Escape 序列 |Microsoft Docs
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
ms.openlocfilehash: 62745b749870fa33151fc1a5f6bd3a1bfc344ad7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429310"
---
# <a name="escape-sequences-in-odbc"></a>ODBC 中的逸出序列
許多語言功能（例如外部聯結和純量函式呼叫）通常是由 Dbms 所執行。 不過，這些功能的語法通常會是 DBMS 特定的，即使標準語法是由各種標準主體所定義也一樣。 因此，ODBC 會定義包含下列語言功能標準語法的 escape 序列：  
  
-   日期、時間、時間戳記和日期時間間隔常值  
  
-   純量函數，例如數值、字串和資料類型轉換函數  
  
-   LIKE 述詞 escape 字元  
  
-   外部聯結  
  
-   程序呼叫  
  
 ODBC 所使用的 escape 順序如下所示：  
  
```  
  
(extension)  
  
```  
  
## <a name="remarks"></a>備註  
 Escape 序列是由驅動程式辨識和剖析，這會使用 DBMS 特定文法來取代 escape 序列。 如需有關 escape sequence 語法的詳細資訊，請參閱附錄 C： SQL 文法中的 [ODBC Escape 序列](../../../odbc/reference/appendixes/odbc-escape-sequences.md) 。  
  
> [!NOTE]  
>  在 ODBC 2 中。*x*，這是 escape 順序的標準語法： **-- (\* 廠商 (**_廠商名稱_**) 、產品 (**_產品名稱_**) **_延伸_ ** \*) --**  
>   
>  除了此語法之外，還定義了下列格式的速記語法：            **{**_extension_**}**  
>   
>  在 ODBC 3 中。*x*，escape 序列的完整格式已被取代，而且縮寫格式是以獨佔方式使用。  
  
 因為 escape 序列是由驅動程式對應至 DBMS 特定的語法，所以應用程式可以使用 escape 序列或 DBMS 特定的語法。 不過，使用 DBMS 特定語法的應用程式將無法互通。 使用 escape 序列時，應用程式應該確定已關閉 SQL_ATTR_NOSCAN 語句屬性（預設為關閉）。 否則，會將 escape 序列直接傳送到資料來源，通常會造成語法錯誤。  
  
 驅動程式只支援它們可對應至基礎語言功能的 escape 序列。 例如，如果資料來源不支援外部聯結，驅動程式就不會有此驅動程式。 為了判斷支援哪些 escape 序列，應用程式會呼叫 **SQLGetTypeInfo** 和 **SQLGetInfo**。 如需詳細資訊，請參閱下一節、 [日期、時間和時間戳記常](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)值。  
  
 此章節包含下列主題。  
  
-   [日期、時間和時間戳記常值](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)  
  
-   [純量函式呼叫](../../../odbc/reference/develop-app/scalar-function-calls.md)  
  
-   [LIKE 述詞逸出字元](../../../odbc/reference/develop-app/like-predicate-escape-character.md)  
  
-   [外部聯結](../../../odbc/reference/develop-app/outer-joins.md)  
  
-   [程序呼叫](../../../odbc/reference/develop-app/procedure-calls.md)
