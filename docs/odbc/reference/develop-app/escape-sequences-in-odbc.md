---
title: ODBC 中的逸出序列 :微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300418"
---
# <a name="escape-sequences-in-odbc"></a>ODBC 中的逸出序列
許多語言功能(如外部聯接和標量函數調用)通常由 DBMS 實現。 但是,這些功能的語法往往特定於 DBMS,即使標準語法由各種標準機構定義也是如此。 因此,ODBC 定義了包含以下語言功能的標準語法的轉義序列:  
  
-   日期、時間、時間戳和日期時間間隔文字  
  
-   標量函數,如數位、字串和資料類型轉換函數  
  
-   喜歡謂詞轉義字元  
  
-   外部聯結  
  
-   程序呼叫  
  
 ODBC 使用的逸出序列的標題:  
  
```  
  
(extension)  
  
```  
  
## <a name="remarks"></a>備註  
 轉義序列由驅動程式識別和解析,這些驅動程式將轉義序列替換為特定於 DBMS 的語法。 有關轉義序列語法的詳細資訊,請參閱附錄 C 中的[ODBC 轉義序列](../../../odbc/reference/appendixes/odbc-escape-sequences.md):SQL 語法。  
  
> [!NOTE]  
>  在 ODBC 2 中。*x*,這是轉義序列的標準語法: **-- (\*供應商(供應商**_名稱_**),產品(**_產品名稱_**)**_擴展_**\*) --**  
>   
>  除了此語法之外,還定義了表單的速記語法: {**擴展**_extension_**}**  
>   
>  在 ODBC 3 中。*x*,轉義序列的長形式已被棄用,速記形式被專門使用。  
  
 由於轉義序列由驅動程式映射到特定於 DBMS 的語法,因此應用程式可以使用轉義序列或特定於 DBMS 的語法。 但是,使用特定於 DBMS 的語法的應用程式將不可互通。 使用轉義序列時,應用程式應確保SQL_ATTR_NOSCAN語句屬性已關閉,預設情況下,該屬性是關閉的。 否則,轉義序列將直接發送到數據源,它通常會導致語法錯誤。  
  
 驅動程式僅支援可以映射到基礎語言要素的轉義序列。 例如,如果數據源不支援外部聯接,則驅動程式也不會。 要確定哪些轉義序列受支援,應用程式呼叫**SQLGetTypeInfo**和**SQLGetInfo**。 有關詳細資訊,請參閱下一節"[日期、時間和時間戳文本](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)"。  
  
 此章節包含下列主題。  
  
-   [日期、時間和時間戳記常值](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)  
  
-   [純量函式呼叫](../../../odbc/reference/develop-app/scalar-function-calls.md)  
  
-   [LIKE 述詞逸出字元](../../../odbc/reference/develop-app/like-predicate-escape-character.md)  
  
-   [外部聯結](../../../odbc/reference/develop-app/outer-joins.md)  
  
-   [程序呼叫](../../../odbc/reference/develop-app/procedure-calls.md)
