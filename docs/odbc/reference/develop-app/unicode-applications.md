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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 94bd5211c878904453624adb2acd0fe435ebc812
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298944"
---
# <a name="unicode-applications"></a>Unicode 應用程式
您可以使用下列兩種方式之一，將應用程式重新編譯成 Unicode 應用程式：  
  
-   將 Unicode **#define**包含在應用程式的 sqlucode.h 標頭檔中。  
  
-   使用編譯器的 Unicode 選項編譯應用程式。 （不同的編譯器會有不同的選項）。  
  
 若要將 ANSI 應用程式轉換成 Unicode 應用程式，請撰寫應用程式來儲存和傳遞 Unicode 資料。 此外，支援 SQLPOINTER 引數之函式的呼叫必須轉換成使用位元組計數。  
  
 將應用程式編譯為 Unicode 應用程式之後，如果應用程式呼叫 ODBC API 函式（不含尾碼），驅動程式管理員會將應用程式辨識為 Unicode 應用程式，並將函式呼叫轉換成 Unicode 函式（使用*W*後置詞）（如果基礎驅動程式支援 unicode）。 當 ANSI 應用程式不使用後置詞進行函式呼叫時，如果基礎驅動程式支援 ANSI，驅動程式管理員會將它轉換成 ANSI。 如果應用程式和驅動程式都支援相同的字元編碼，驅動程式管理員會將呼叫傳遞至驅動程式（但 ANSI 應用程式有特定例外狀況）。  
  
 應用程式可以同時呼叫 Unicode 函式（使用*W*後置詞）和 ANSI 函數（不論是否*有尾碼）* 。 Unicode 和 ANSI 函式呼叫可以混合。 不過，如果要使用資料指標程式庫，則 Unicode 和 ANSI 函式呼叫無法混合。 資料指標程式庫可以是 Unicode 或 ANSI，而不是混合。  
  
 您可以撰寫應用程式，讓它可以編譯成 Unicode 應用程式或 ANSI 應用程式。 在此情況下，字元資料類型可以宣告為 SQL_C_TCHAR。 這個宏會在應用程式編譯為 Unicode 應用程式時插入 SQL_C_WCHAR，如果編譯為 ANSI 應用程式，則插入 SQL_C_CHAR。 應用程式設計人員必須謹慎使用 SQLPOINTER 做為其引數的函式，因為 length 引數的大小會隨著應用程式是 ANSI 或 Unicode 而變更（針對字串資料類型）。  
  
 函式可透過下列三種方式的其中一種來呼叫：當做僅限 Unicode 的函式呼叫（含*W*後置字元），做為僅限 ANSI 函式呼叫（*含尾碼）* ，或做為不含後置字元的 ODBC 函式呼叫。 函式的三種形式的引數完全相同。 只有包含 SQLCHAR \*引數的函式或指向字串的 SQLPOINTER 引數，才需要 UNICODE 和 ANSI 格式。 對於具有可宣告為字元類型之引數的函式（例如**SQLBindCol**或**SQLGetData** （不具有 Unicode 和 ANSI 格式），引數可以宣告為 Unicode 類型、ANSI 類型，或在 C 類型引數的情況下，SQL_C_TCHAR 宏。 如需詳細資訊，請參閱[Unicode 資料](../../../odbc/reference/develop-app/unicode-data.md)。  
  
 應用程式可以撰寫成 Unicode 應用程式，即使沒有任何 Unicode 驅動程式可供使用也一樣。 驅動程式管理員會將 Unicode 函數和資料類型對應到 ANSI。 可以執行的 Unicode 與 ANSI 對應有一些限制。 Unicode 驅動程式是否存在，以供使用會導致效能更佳，並會移除 Unicode 與 ANSI 對應的固有限制。
