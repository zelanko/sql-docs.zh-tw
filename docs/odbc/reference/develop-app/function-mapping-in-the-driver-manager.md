---
title: "函式對應驅動程式管理員在 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Unicode [ODBC], functions
- driver manager [ODBC], function mapping
- functions [ODBC], Unicode functions
ms.assetid: ff093b29-671a-4fc0-86c9-08a311a98e54
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 63c908b668e4cecd93cc9930f638ccde9173b563
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="function-mapping-in-the-driver-manager"></a>函式對應驅動程式管理員
驅動程式管理員支援兩個進入點，接受字串引數的函式。 未裝飾的函式 (**SQLDriverConnect**) 是 ANSI 格式的函式。 以 Unicode 格式裝飾*W* (**SQLDriverConnectW**。)  
  
 也支援 ODBC 標頭檔的函式以裝飾*A，* (**SQLDriverConnectA**) 方便的混合的 ANSI/Unicode 應用程式。 對呼叫**A**函式是實際的未裝飾的進入點的呼叫 (**SQLDriverConnect**。)  
  
 如果應用程式編譯 _UNICODE **#define**，ODBC 標頭檔會將對應的未裝飾的函式呼叫 (**SQLDriverConnect**) 的 Unicode 版本 (**SQLDriverConnectW**.)  
  
 驅動程式管理員可辨識驅動程式作為 Unicode 驅動程式如果**SQLConnectW**驅動程式支援。  
  
 如果驅動程式是 Unicode，驅動程式管理員會函式呼叫，如下所示：  
  
-   將沒有字串引數或參數的函式直接透過傳遞至驅動程式。  
  
-   傳遞 Unicode 函式 (具有*W*尾碼) 直接透過驅動程式。  
  
-   ANSI 函式會將轉換 (與*A*後置詞) 的 Unicode 函式 (與*W*尾碼) 將字串引數轉換成 Unicode 字元，並將 Unicode 函式傳遞至驅動程式。  
  
 如果驅動程式是 ANSI 驅動程式，驅動程式管理員會函式呼叫，如下所示：  
  
-   將函式，而不需要字串引數或透過直接參數傳遞至驅動程式。  
  
-   轉換 Unicode 函式 (具有*W*尾碼) 成 ANSI 函式呼叫，並將其傳遞至驅動程式。  
  
-   ANSI 函式會直接傳遞至驅動程式。  
  
 驅動程式管理員已啟用 Unicode 內部。 如此一來，最佳的效能，來取得在 Unicode 應用程式使用 Unicode 的驅動程式，因為驅動程式管理員只會將 Unicode 函式透過傳遞至驅動程式。 當 ANSI 驅動程式會使用 ANSI 應用程式時，驅動程式管理員必須將字串轉換從 ANSI 為 Unicode 時處理某些函式，例如**SQLDriverConnect**。 之後處理函式，驅動程式管理員必須再將轉換的 Unicode 字串回 ANSI ANSI 驅動程式傳送函式之前。  
  
 應用程式不應該修改或驅動程式傳回 SQL_STILL_EXECUTING 或 SQL_NEED_DATA 時讀取其繫結的參數緩衝區。 驅動程式管理員會保留緩衝區繫結為 ANSI，直到驅動程式傳回 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO 或 SQL_ERROR。 多執行緒應用程式不應該存取另一個執行緒上執行 SQL 陳述式的任何繫結的參數值。 驅動程式管理員將資料從 Unicode 轉換成 ANSI"就地，」，另一個執行緒可能會看到這些緩衝區中的 ANSI 資料時，驅動程式仍在處理 SQL 陳述式。 Unicode 資料繫結至 ANSI 驅動程式的應用程式必須兩個不同的資料行繫結至相同的位址。
