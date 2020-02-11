---
title: 緩衝區 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- input buffers [ODBC]
- length/indicator buffers [ODBC]
- output buffers [ODBC]
- buffers [ODBC], about buffers
- application buffers [ODBC]
- buffers [ODBC]
ms.assetid: 42c5226c-cb40-4d1e-809f-2ea50ce6bd55
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ad13379552e3a5a576b0aa5cc8720ca6ca1688a9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68118737"
---
# <a name="buffers"></a>緩衝區
緩衝區是用來在應用程式和驅動程式之間傳遞資料的任何應用程式記憶體片段。 例如，應用程式緩衝區可以與**SQLBindCol**相關聯或系結*至*結果集資料行。 提取每個資料列時，會針對這些緩衝區中的每個資料行傳回資料。 *輸入緩衝區*是用來將資料從應用程式傳遞至驅動程式;*輸出緩衝區*是用來將驅動程式的資料傳回給應用程式。  
  
> [!NOTE]  
>  如果 ODBC 函數傳回 SQL_ERROR，該函式的任何輸出引數內容都是未定義的。  
  
 這項討論主要著重于不確定類型的緩衝區。 這些緩衝區的位址會顯示為 SQLPOINTER 類型的引數，例如**SQLBindCol**中的*TargetValuePtr*引數。 不過，這裡所討論的某些專案（例如與緩衝區搭配使用的引數）也適用于將字串傳遞至驅動程式所使用的引數，例如**SQLTables**中的*TableName*引數。  
  
 這些緩衝區通常成對。 *資料緩衝區*是用來傳遞資料本身，而*長度/指標緩衝區*則是用來傳遞資料緩衝區中的資料長度或特殊值（例如 SQL_Null_DATA），這表示資料是 Null。 資料緩衝區中的資料長度與資料緩衝區本身的長度不同。 下圖顯示資料緩衝區與長度/指標緩衝區之間的關聯性。  
  
 ![資料緩衝區和長度&#47;指標緩衝區](../../../odbc/reference/develop-app/media/pr09.gif "pr09")  
  
 每當資料緩衝區包含可變長度的資料（例如字元或二進位資料）時，就需要長度/指標緩衝區。 如果資料緩衝區包含固定長度的資料（例如整數或日期結構），則只需要長度/指標緩衝區來傳遞指標值，因為資料的長度已經是已知的。 如果應用程式使用長度/指標緩衝區搭配固定長度的資料，驅動程式會忽略其中傳遞的任何長度。  
  
 資料緩衝區和其所包含資料的長度是以位元組為單位來測量，而不是字元。 對於使用 ANSI 字串的程式而言，這項區別並不重要，因為位元組和字元的長度都相同。  
  
 當資料緩衝區代表驅動程式定義的描述項欄位、診斷欄位或屬性時，應用程式應該向驅動程式管理員指出指出欄位或屬性值的函數引數的本質。 應用程式會在將欄位或屬性設定為下列其中一個值的任何函數呼叫中設定長度引數，藉此執行此動作。 （這也適用于抓取欄位或屬性值的函式，但引數指向設定函式本身的值則是例外）。  
  
-   如果指出欄位或屬性值的函式引數是字元字串的指標，則*length*引數會是字串或 SQL_NTS 的長度。  
  
-   如果指出欄位或屬性值的函式引數是二進位緩衝區的指標，應用程式會將 SQL_LEN_BINARY_ATTR （*長度*）宏的結果放在*length*引數中。 這會在*length*引數中放置負數值。  
  
-   如果指出欄位或屬性值的函式引數是字元字串或二進位字串以外的值指標，則*length*引數應該具有值 SQL_IS_POINTER。  
  
-   如果指出欄位或屬性值的函式引數包含固定長度的值，則*長度*引數會 SQL_IS_INTEGER、SQL_IS_UINTEGER、SQL_IS_SMALLINT 或 SQL_ISI_USMALLINT （視情況而定）。  
  
 此章節包含下列主題。  
  
-   [延遲的緩衝區](../../../odbc/reference/develop-app/deferred-buffers.md)  
  
-   [配置及釋放緩衝區](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)  
  
-   [使用資料緩衝區](../../../odbc/reference/develop-app/using-data-buffers.md)
