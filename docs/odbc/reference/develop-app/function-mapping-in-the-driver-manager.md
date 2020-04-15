---
title: 驅動程式管理員中的功能映射 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC], functions
- driver manager [ODBC], function mapping
- functions [ODBC], Unicode functions
ms.assetid: ff093b29-671a-4fc0-86c9-08a311a98e54
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: db8e525bb7e8f3e167deb8061a4dd5b75073933c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305579"
---
# <a name="function-mapping-in-the-driver-manager"></a>驅動程式管理員中的函式對應
驅動程式管理員支援具有字串參數的函數的兩個入口點。 未修飾函數 (**SQLDriverConnect**) 是函數的 ANSI 形式. Unicode 窗體用**W(SQLDriverConnectW** *W* )裝飾。  
  
 ODBC 標頭檔支援使用*A(* **SQLDriverConnectA**) 修飾的功能,以方便混合 ANSI/Unicode 應用程式。 對**A**函數進行的調用實際上是對未修飾的入口點 **(SQLDriverConnect**)的調用。  
  
 如果應用程式使用 **_UNICODE#define**編譯,則 ODBC 標頭檔將未修飾的函數呼叫 **(SQLDriverConnect)** 映射到 Unicode 版本 **(SQLDriverConnectW**).  
  
 如果驅動程式支援**SQLConnectW,** 驅動程式管理器會將驅動程式識別為 Unicode 驅動程式。  
  
 如果驅動程式是 Unicode 驅動程式,驅動程式管理員會按照如下方式進行函數呼叫:  
  
-   將沒有字串參數或參數的函數直接傳遞給驅動程式。  
  
-   將 Unicode 函數(帶*W*後綴)直接傳遞到驅動程式。  
  
-   通過將字串參數轉換為 Unicode 字元並將 Unicode 函數傳遞給驅動程式,將 ANSI 函數(帶*A*後綴)轉換為 Unicode 函數(帶*W*後置)。  
  
 如果驅動程式是 ANSI 驅動程式,則驅動程式管理員進行函數呼叫,如下所示:  
  
-   將沒有字串參數或參數的函數直接傳遞給驅動程式。  
  
-   將 Unicode 函數(帶*W*後置)轉換為 ANSI 函數調用,並將其傳遞給驅動程式。  
  
-   將 ANSI 函數直接傳遞給驅動程式。  
  
 驅動程式管理員在內部啟用 Unicode。 因此,使用 Unicode 驅動程式的 Unicode 應用程式獲得了最佳性能,因為驅動程式管理器只需將 Unicode 函數傳遞給驅動程式即可。 當 ANSI 應用程式使用 ANSI 驅動程式時,驅動程式管理器在處理某些函數(如**SQLDriverConnect**)時,必須將字串從 ANSI 轉換為 Unicode。 處理函數後,驅動程式管理員必須將 Unicode 字串轉換回 ANSI,然後再將函數發送到 ANSI 驅動程式。  
  
 當驅動程式返回SQL_STILL_EXECUTING或SQL_NEED_DATA時,應用程式不應修改或讀取其綁定參數緩衝區。 驅動程式管理員將緩衝區綁定到 ANSI,直到驅動程式返回SQL_SUCCESS、SQL_SUCCESS_WITH_INFO或SQL_ERROR。 多線程應用程式不應存取另一個線程正在執行 SQL 語句的任何綁定參數值。 驅動程式管理員將資料從 Unicode 轉換為 ANSI"就位",另一個線程可能會在這些緩衝區中看到 ANSI 資料,而驅動程式仍在處理 SQL 語句。 將 Unicode 資料繫結到 ANSI 驅動程式的應用程式不得將兩個不同的列綁定到同一位址。
