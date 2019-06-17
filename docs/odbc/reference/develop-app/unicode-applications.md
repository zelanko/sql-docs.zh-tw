---
title: Unicode 應用程式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC], compiling as Unicode application
- Unicode [ODBC], functions
- compiling Unicode applications [ODBC]
- functions [ODBC], Unicode functions
ms.assetid: 7986c623-2792-4e77-bfee-c86cbf84f08d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7fc9cb98837d206d5279d1f14d4a57ce56782759
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62633378"
---
# <a name="unicode-applications"></a>Unicode 應用程式
您可以重新編譯應用程式成為 Unicode 應用程式中有兩種：  
  
-   包含 Unicode **#define**包含 Sqlucode.h 標頭檔，應用程式中。  
  
-   編譯應用程式的編譯器 [Unicode] 選項。 （這個選項會針對其他編譯器不同。）  
  
 若要轉換的 ANSI 應用程式，以在 Unicode 應用程式，撰寫應用程式來儲存和傳遞 Unicode 資料。 此外，支援 SQLPOINTER 引數的函式呼叫必須轉換成使用的位元組計數。  
  
 如果應用程式呼叫 ODBC API 函式 （沒有尾碼），將會編譯為 Unicode 應用程式的應用程式之後，驅動程式管理員會辨識為 Unicode 應用程式的應用程式，並將轉換函式呼叫至 Unicode 的函式 （ *W*後置詞) 如果基礎驅動程式支援 Unicode。 當 ANSI 應用程式提出呼叫沒有尾碼的函式時，驅動程式管理員將它轉換成 ANSI 如果基礎驅動程式支援 ANSI。 如果應用程式和驅動程式支援相同的字元編碼，驅動程式管理員會將呼叫傳遞給將驅動程式 （與 ANSI 應用程式特定例外狀況）。  
  
 應用程式可以呼叫這兩個 Unicode 函式 (具有*W*後置詞) 和 ANSI 函式 (包含或不含*A*尾碼)。 可以混合使用 Unicode 和 ANSI 函式呼叫。 如果資料指標程式庫是使用，不過，Unicode 和 ANSI 函式呼叫不能混合。 資料指標程式庫是 Unicode 或 ANSI，無法混用。  
  
 可以撰寫應用程式，使它可以編譯成 Unicode 應用程式或 ANSI 應用程式。 在此情況下，字元資料類型可以宣告為 SQL_C_TCHAR。 這是插入 SQL_C_WCHAR，如果應用程式編譯成 Unicode 應用程式，或如果它編譯為 ANSI 應用程式，插入 SQL_C_CHAR 巨集。 應用程式設計人員必須小心做為其引數，不接受 SQLPOINTER 函式的因為長度的引數的大小會變更 （適用於字串資料類型） 根據應用程式為 ANSI 或 Unicode。  
  
 函式可以呼叫在三種方式之一： 為僅限 Unicode 的函式呼叫 (使用*W*後置詞)，為僅限 ANSI 函式呼叫 (與*A*尾碼)，或沒有後置詞的 ODBC 函式呼叫。 三種形式的函式的引數都相同。 只有這些函式中的以 SQLCHAR\*引數或指向字串的 SQLPOINTER 引數需要 Unicode 和 ANSI 形式。 有可以宣告為字元類型，例如的引數的函式**SQLBindCol**或是**SQLGetData** （其中沒有 Unicode 和 ANSI 形式），引數可以宣告為 Unicode 類型，ANSI 類型，或如果 C 是輸入引數，SQL_C_TCHAR 巨集。 如需詳細資訊，請參閱 < [Unicode 資料](../../../odbc/reference/develop-app/unicode-data.md)。  
  
 應用程式可以撰寫為 Unicode 應用程式，即使沒有 Unicode 驅動程式可用，才能使用。 驅動程式管理員會對應至 ANSI 的 Unicode 函式和資料類型。 有一些限制可以執行的 ANSI 對應至 unicode。 Unicode 應用程式來使用的 Unicode 驅動程式存在會導致更好的效能，並會移除的 ANSI 對應至 Unicode 的固有的限制。
