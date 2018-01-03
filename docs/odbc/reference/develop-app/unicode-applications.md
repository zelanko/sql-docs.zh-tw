---
title: "Unicode 應用程式 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Unicode [ODBC], compiling as Unicode application
- Unicode [ODBC], functions
- compiling Unicode applications [ODBC]
- functions [ODBC], Unicode functions
ms.assetid: 7986c623-2792-4e77-bfee-c86cbf84f08d
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7bc4228f693f2d5753c3b04cf6e2cd48e18a591b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="unicode-applications"></a>Unicode 應用程式
您可以重新編譯應用程式中有兩種在 Unicode 應用程式：  
  
-   包含 Unicode **#define**包含 Sqlucode.h 標頭檔，應用程式中。  
  
-   編譯應用程式使用編譯器的 Unicode 選項。 （這個選項會因不同的編譯器的。）  
  
 若要轉換在 Unicode 應用程式的 ANSI 應用程式，撰寫應用程式來儲存和傳遞 Unicode 資料。 此外，支援 SQLPOINTER 引數的函式的呼叫必須轉換成使用的位元組計數。  
  
 如果應用程式呼叫 ODBC API 函式 （沒有尾碼），將會編譯為 Unicode 應用程式的應用程式之後，驅動程式管理員會辨識 Unicode 應用程式的應用程式，並將轉換至 Unicode 的函式 （函式呼叫*W*尾碼) 如果此基礎驅動程式支援 Unicode。 函式呼叫而不需要後置字元的 ANSI 應用程式時，驅動程式管理員將它轉換成 ANSI 如果基礎驅動程式支援 ANSI。 如果應用程式和驅動程式支援相同的字元編碼，驅動程式管理員會傳遞到 （使用 ANSI 應用程式特定例外狀況） 的驅動程式透過呼叫。  
  
 應用程式可以呼叫這兩個 Unicode 函式 (具有*W*後置詞) 和 ANSI 函式 (含*A*後置詞)。 可以混合 Unicode 和 ANSI 函式呼叫。 如果資料指標程式庫是使用，不過，Unicode 和 ANSI 函式呼叫不能混合。 資料指標程式庫是 Unicode 或 ANSI，無法混合。  
  
 可以撰寫應用程式，使它可以編譯為在 Unicode 應用程式或 ANSI 應用程式。 在此情況下，字元資料類型可以宣告為 SQL_C_TCHAR。 這是插入 SQL_C_WCHAR，如果應用程式會編譯為在 Unicode 應用程式，或插入 SQL_C_CHAR 就會編譯為 ANSI 應用程式的巨集。 應用程式設計者必須非常小心，當做其引數，不接受 SQLPOINTER 函式的由於長度的引數的大小將會變更 （適用於字串資料類型） 視應用程式為 ANSI 或 Unicode。  
  
 函式可以呼叫其中一種方式： 做為僅限 Unicode 的函式呼叫 (與*W*尾碼)，為 ANSI 專用函式呼叫 (與*A*尾碼)，或沒有後置詞的 ODBC 函數呼叫。 函式的三種形式的引數都相同。 這些函數與 SQLCHAR\*引數或指向字串的 SQLPOINTER 引數需要 Unicode 和 ANSI 表單。 對於函式的引數可以宣告為字元類型，例如**SQLBindCol**或**SQLGetData** （這不需要 Unicode 和 ANSI 表單），引數可以宣告為 Unicode 類型，ANSI 類型，或在 C 的情況下型別引數，SQL_C_TCHAR 巨集。 如需詳細資訊，請參閱[Unicode 資料](../../../odbc/reference/develop-app/unicode-data.md)。  
  
 應用程式可以撰寫成在 Unicode 應用程式，即使沒有 Unicode 驅動程式可供它使用。 驅動程式管理員會為 ANSI 對應 Unicode 函式和資料類型。 有一些限制可以執行的 ANSI 對應至 unicode。 Unicode 應用程式來使用的 Unicode 驅動程式存在會導致更好的效能，所以會移除固有的 ANSI 對應至 Unicode 的限制。
