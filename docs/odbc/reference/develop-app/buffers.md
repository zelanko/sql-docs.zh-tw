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
manager: craigg
ms.openlocfilehash: 306632f544f144aa4b21e150543c2d4ca5a37d0e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47820026"
---
# <a name="buffers"></a>緩衝區
緩衝區是記憶體的任何應用程式所使用的應用程式和驅動程式之間傳遞資料。 例如，應用程式緩衝區可以與其產生關聯，或 *，繫結*結果集資料行**SQLBindCol**。 擷取每個資料列，因為在這些緩衝區中的每個資料行就會傳回資料。 *輸入緩衝區*用來將資料傳遞至驅動程式; 應用程式*輸出緩衝區*用來從驅動程式應用程式將資料傳回。  
  
> [!NOTE]  
>  如果 ODBC 函數會傳回 SQL_ERROR，該函式的任何輸出引數的內容為未定義。  
  
 在本文中有關本身，主要是以不確定類型的緩衝區。 這些緩衝區的位址會顯示為引數的型別 SQLPOINTER，這類*TargetValuePtr*中的引數**SQLBindCol**。 不過，某些的討論，例如緩衝區，搭配使用的引數的項目也適用於用來將字串傳遞至驅動程式，例如引數*TableName*中的引數**SQLTables**。  
  
 這些緩衝區通常有配對。 *資料緩衝區*是用來傳遞資料本身，而*長度/指標緩衝區*用來傳遞的資料緩衝區或例如 SQL_NULL_DATA 表示資料為 NULL 的特殊值中的資料長度。 資料緩衝區中資料的長度是從本身的資料緩衝區的長度不同。 下圖顯示的資料緩衝區和長度/指標緩衝區之間的關聯性。  
  
 ![資料緩衝區和長度&#47;指標緩衝區](../../../odbc/reference/develop-app/media/pr09.gif "pr09")  
  
 每當資料緩衝區包含可變長度的資料，例如字元或二進位資料時需要長度/指標緩衝區。 如果資料緩衝區會包含固定長度的資料，例如整數或日期的結構，長度/指標緩衝區只被為了傳遞指標值，因為資料的長度為已知。 如果應用程式使用的固定長度資料的長度/指標緩衝區，驅動程式會忽略任何傳遞它的長度。  
  
 長度的資料緩衝區和它所包含的資料被以位元組為單位，而不是字元。 這項區別並不重要的使用 ANSI 字串，因為在位元組和字元的長度是相同的程式。  
  
 當資料緩衝區表示驅動程式定義的描述項欄位、 診斷的欄位或屬性時，應用程式應該指出驅動程式管理員本質函式引數，表示欄位或屬性的值。 應用程式的運作方式將欄位或屬性設定為下列值之一的任何函式呼叫中設定的長度引數。 （這也適用於擷取值的欄位或屬性，且引數指向的值設定函式的引數本身中的例外狀況的函式。）  
  
-   如果表示欄位或屬性的值的函式引數是字元字串的指標*長度*引數是 sql_nts; 之字串的長度。  
  
-   表示欄位或屬性的值的函式引數是二進位緩衝區的指標，如果應用程式會將 SQL_LEN_BINARY_ATTR 的結果 (*長度*) 中的巨集*長度*引數。 這會放在負值*長度*引數。  
  
-   如果函式引數，表示欄位或屬性的值以外的字元字串或二進位字串值的指標*長度*引數應該有 SQL_IS_POINTER 的值。  
  
-   表示欄位或屬性的值的函式引數包含固定長度的值，如果*長度*引數是 SQL_IS_INTEGER、 SQL_IS_UINTEGER、 SQL_IS_SMALLINT，還是 SQL_ISI_USMALLINT，適當地。  
  
 此章節包含下列主題。  
  
-   [延遲的緩衝區](../../../odbc/reference/develop-app/deferred-buffers.md)  
  
-   [配置及釋放緩衝區](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)  
  
-   [使用資料緩衝區](../../../odbc/reference/develop-app/using-data-buffers.md)
