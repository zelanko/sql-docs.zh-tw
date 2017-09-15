---
title: "逸出序列在 ODBC |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- escape sequences [ODBC]
- SQL statements [ODBC], escape sequences
- escape sequences [ODBC], about escape sequences
ms.assetid: cf229f21-6c38-4b5b-aca8-f1be0dfeb3d0
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 92fd9745bccacad3d7487c3ed9f1bee58eeb4411
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="escape-sequences-in-odbc"></a>在 ODBC 中的逸出序列
數字的語言功能，例如外部聯結和純量函式呼叫，通常是由 Dbms 實作。 不過，這些功能的語法通常 DBMS 專屬的即使標準語法定義各種標準組織所。 因為這個緣故，ODBC 會定義包含下列語言功能的標準語法的逸出序列：  
  
-   日期、 時間、 時間戳記和日期時間間隔的常值  
  
-   純量函數，例如數字、 字串和資料類型轉換函式  
  
-   喜歡述詞的逸出字元  
  
-   外部聯結  
  
-   程序呼叫  
  
 ODBC 所使用的逸出順序如下所示：  
  
```  
  
(extension)  
  
```  
  
## <a name="remarks"></a>備註  
 逸出序列會辨識並剖析驅動程式，逸出序列取代特定 DBMS 的文法。 如需逸出序列語法的詳細資訊，請參閱[ODBC 逸出序列](../../../odbc/reference/appendixes/odbc-escape-sequences.md)附錄 c: SQL 文法中。  
  
> [!NOTE]  
>  在 ODBC 2。*x*，這是標準語法的逸出序列： **-(\*廠商 (***廠商名稱***)，產品 (** *產品名稱***)***延伸* ** \*)-**  
>   
>  除了這個語法中，縮寫語法已定義的表單： **{***延伸***}**  
>   
>  在 ODBC 3。*x*逸出序列的完整格式已被取代，且以獨佔方式使用的簡短形式。  
  
 驅動程式新增至 DBMS 特定語法的逸出序列來對應，因為應用程式可以使用的逸出序列 」 或 「 DBMS 特有的語法。 不過，使用 DBMS 特定語法的應用程式將無法互通。 當使用逸出序列時，應用程式應該要確定，SQL_ATTR_NOSCAN 陳述式屬性已關閉，這是預設值。 否則，逸出序列將會直接傳送至資料來源，其中它通常會造成語法錯誤。  
  
 驅動程式支援它們可以將對應至基礎的語言功能的逸出序列。 比方說，如果資料來源不支援外部聯結，兩者都不會將驅動程式。 若要判斷支援哪些逸出序列，應用程式呼叫**SQLGetTypeInfo**和**SQLGetInfo**。 如需詳細資訊，請參閱下節中，[日期、 時間和時間戳記常值](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)。  
  
 此章節包含下列主題。  
  
-   [日期、 時間和時間戳記常值](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)  
  
-   [純量函式呼叫](../../../odbc/reference/develop-app/scalar-function-calls.md)  
  
-   [像述詞的逸出字元](../../../odbc/reference/develop-app/like-predicate-escape-character.md)  
  
-   [外部聯結](../../../odbc/reference/develop-app/outer-joins.md)  
  
-   [程序呼叫](../../../odbc/reference/develop-app/procedure-calls.md)
