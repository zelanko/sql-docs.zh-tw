---
title: 逸出序列，在 ODBC |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3866a45a2b55a5372769eacc0bb6b0eb1e5c088f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62942971"
---
# <a name="escape-sequences-in-odbc"></a>ODBC 中的逸出序列
語言功能，例如外部聯結和純量函式呼叫的數目通常是由 Dbms 實作。 不過，這些功能的語法通常 DBMS 而異，即使是標準的語法由各種不同的標準內文。 因為這個緣故，ODBC 會定義包含下列語言功能的標準語法的逸出序列：  
  
-   日期、 時間、 時間戳記和日期時間間隔常值  
  
-   純量函式，例如包含數字、 字串和資料類型轉換函式  
  
-   讓述詞逸出字元  
  
-   外部聯結  
  
-   程序呼叫  
  
 ODBC 使用的逸出序列如下所示：  
  
```  
  
(extension)  
  
```  
  
## <a name="remarks"></a>備註  
 逸出序列會辨識並剖析驅動程式，逸出序列取代為特定 DBMS 的文法。 如需逸出序列語法的詳細資訊，請參閱[ODBC 逸出序列](../../../odbc/reference/appendixes/odbc-escape-sequences.md)附錄 c:SQL 文法。  
  
> [!NOTE]  
>  在 ODBC 2。*x*，這是逸出序列的標準語法： **-(\*廠商 (**_廠商名稱_**)，產品 (** _產品名稱_**)**_擴充功能_  **\*)-**  
>   
>  這個語法中，除了速記語法定義的格式： **{**_擴充功能_**}**  
>   
>  在 ODBC 3。*x*、 逸出序列的完整格式已被取代，，和以獨佔方式使用簡短形式。  
  
 因為逸出序列會對應特定 DBMS 的語法來驅動程式，應用程式可以使用的逸出序列 」 或 「 特定 DBMS 的語法。 不過，使用的 DBMS 特定語法的應用程式將無法互通。 當使用逸出序列時，應用程式應該要確定，SQL_ATTR_NOSCAN 陳述式屬性已關閉，這是預設值。 否則，逸出序列會直接傳送到資料來源，其中它通常會導致語法錯誤。  
  
 驅動程式支援它們可以對應到基礎的語言功能的逸出序列。 比方說，如果資料來源不支援外部聯結，兩者都不會將驅動程式。 若要判斷支援的逸出序列，應用程式會呼叫**SQLGetTypeInfo**並**SQLGetInfo**。 如需詳細資訊，請參閱下一步 區段中，[日期、 時間和時間戳記常值](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)。  
  
 此章節包含下列主題。  
  
-   [日期、時間和時間戳記常值](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)  
  
-   [純量函式呼叫](../../../odbc/reference/develop-app/scalar-function-calls.md)  
  
-   [LIKE 述詞逸出字元](../../../odbc/reference/develop-app/like-predicate-escape-character.md)  
  
-   [外部聯結](../../../odbc/reference/develop-app/outer-joins.md)  
  
-   [程序呼叫](../../../odbc/reference/develop-app/procedure-calls.md)
