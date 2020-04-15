---
title: 單代碼應用程式 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298944"
---
# <a name="unicode-applications"></a>Unicode 應用程式
您可以透過兩種方式之一會應用程式重新編譯為 Unicode 應用程式:  
  
-   在應用程式中包括 Sqlucode.h 標頭檔中包含的 Unicode **#define。**  
  
-   使用編譯器的 Unicode 選項編譯應用程式。 (對於不同的編譯器,此選項會有所不同。  
  
 要將 ANSI 應用程式轉換為 Unicode 應用程式,請編寫應用程式以儲存和傳遞 Unicode 資料。 此外,對支援 SQLPOINTER 參數的函數的調用必須轉換為位元組的使用計數。  
  
 將應用程式編譯為 Unicode 應用程式後,如果應用程式呼叫 ODBC API 函數(沒有後綴),驅動程式管理員將應用程式辨識為 Unicode 應用程式,如果基礎驅動程式支援 Unicode,則將函數調用轉換為 Unicode 函數(帶*W*後綴)。 當 ANSI 應用程式在沒有後綴的情況下進行函數調用時,如果基礎驅動程式支援 ANSI,驅動程式管理器會將其轉換為 ANSI。 如果應用程式和驅動程式都支援相同的字元編碼,驅動程式管理器會將呼叫傳遞到驅動程式(ANSI 應用程式的某些例外情況除外)。  
  
 應用程式可以同時調用 Unicode 函數(帶*W*後綴)和 ANSI 函數(帶或沒有*A*後綴)。 Unicode 和 ANSI 函數呼用可以混合。 但是,如果要使用游標庫,則不能混合 Unicode 和 ANSI 函數調用。 游標庫是 Unicode 或 ANSI,而不是混合體。  
  
 可以編寫應用程式,以便它可以編譯為 Unicode 應用程式或 ANSI 應用程式。 在這種情況下,字元數據類型可以聲明為SQL_C_TCHAR。 這是一個宏,用於插入SQL_C_WCHAR如果應用程式編譯為 Unicode 應用程式,或者SQL_C_CHAR(如果應用程式編譯為 ANSI 應用程式)插入。 應用程式程式師必須小心以 SQLPOINTER 作為參數的函數,因為長度參數的大小將更改(對於字串資料類型),具體取決於應用程式是 ANSI 還是 Unicode。  
  
 函數可以通過以下三種方式之一調用:作為僅 Unicode 函數調用(帶有*W*後綴)、僅 ANSI 函數調用(帶*A*後綴)或作為沒有後綴的 ODBC 函數調用。 函數的三種形式的參數是相同的。 只有具有 SQLCHAR\*參數或指向字串的 SQLPOINTER 參數的函數才需要 Unicode 和 ANSI 窗體。 對於具有可聲明為字元類型的參數的函數(如**SQLBindCol**或**SQLGetData(** 沒有 Unicode 和 ANSI 窗體),可以將參數聲明為 Unicode 類型、ANSI 類型,或者對於 C 類型參數(SQL_C_TCHAR宏)。 有關詳細資訊,請參閱[Unicode 資料](../../../odbc/reference/develop-app/unicode-data.md)。  
  
 即使沒有 Unicode 驅動程式可供它使用,也可以將應用程式編寫為 Unicode 應用程式。 驅動程式管理員將 Unicode 函數和資料類型映射到 ANSI。 可以對 UNIcode 到 ANSI 映射進行一些限制。 Unicode 應用程式使用 Unicode 驅動程式將提供更好的性能,並將消除 Unicode 到 ANSI 映射中固有的限制。
