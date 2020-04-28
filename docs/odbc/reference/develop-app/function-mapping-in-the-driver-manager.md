---
title: 驅動程式管理員中的函數對應 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305579"
---
# <a name="function-mapping-in-the-driver-manager"></a>驅動程式管理員中的函式對應
驅動程式管理員支援採用字串引數之函式的兩個進入點。 未修飾函式（**SQLDriverConnect**）是函式的 ANSI 形式。 Unicode 格式會以*W* （**SQLDriverConnectW**）裝飾。  
  
 ODBC 標頭檔也支援以*A、* （**SQLDriverConnectA**）裝飾的函式，以方便混合 ANSI/Unicode 應用程式。 對函式所**做的呼叫**實際上會呼叫未修飾的進入點（**SQLDriverConnect**）。  
  
 如果應用程式是使用 _UNICODE **#define**進行編譯，則 ODBC 標頭檔會將未裝飾的函式呼叫（**SQLDriverConnect**）對應到 UNICODE 版本（**SQLDriverConnectW**）。  
  
 如果驅動程式支援**SQLConnectW** ，驅動程式管理員會將驅動程式辨識為 Unicode 驅動程式。  
  
 如果驅動程式是 Unicode 驅動程式，驅動程式管理員會進行函數呼叫，如下所示：  
  
-   將沒有字串引數或參數的函式直接傳遞至驅動程式。  
  
-   將 Unicode 函式（含*W*尾碼）直接傳遞至驅動程式。  
  
-   藉由將字串引數轉換*A*成 unicode 字元，並將 unicode 函式傳遞給驅動程式，將 ANSI 函式（含後置詞）轉換成 unicode 函數（使用*W*尾碼）。  
  
 如果驅動程式是 ANSI 驅動程式，驅動程式管理員會進行函數呼叫，如下所示：  
  
-   將沒有字串引數或參數的函式直接傳遞至驅動程式。  
  
-   將 Unicode 函式（含*W*後置字元）轉換為 ANSI 函式呼叫，並將其傳遞給驅動程式。  
  
-   將 ANSI 函數直接傳遞至驅動程式。  
  
 驅動程式管理員在內部啟用 Unicode。 因此，使用 Unicode 驅動程式的 Unicode 應用程式會取得最佳效能，因為驅動程式管理員只會將 Unicode 函式傳遞至驅動程式。 當 ANSI 應用程式使用 ANSI 驅動程式時，驅動程式管理員必須在處理某些函式（例如**SQLDriverConnect**）時，將字串從 ANSI 轉換成 Unicode。 處理函式之後，驅動程式管理員必須先將 Unicode 字串轉換回 ANSI，然後再將函數傳送至 ANSI 驅動程式。  
  
 當驅動程式傳回 SQL_STILL_EXECUTING 或 SQL_NEED_DATA 時，應用程式不應該修改或讀取其系結的參數緩衝區。 驅動程式管理員會保留系結至 ANSI 的緩衝區，直到驅動程式傳回 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO 或 SQL_ERROR 為止。 多執行緒應用程式不應取得另一個執行緒在上執行 SQL 語句之任何系結參數值的存取權。 驅動程式管理員會將資料從 Unicode 轉換成 ANSI，而另一個執行緒可能會在驅動程式仍在處理 SQL 語句時，看到這些緩衝區中的 ANSI 資料。 系結 Unicode 資料至 ANSI 驅動程式的應用程式，不能將兩個不同的資料行系結至相同的位址。
