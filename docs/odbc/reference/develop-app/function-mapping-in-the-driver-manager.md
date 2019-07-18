---
title: 函式對應在驅動程式管理員 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2bfa535d4175c109e96098dd1e40e93be9521de2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68069693"
---
# <a name="function-mapping-in-the-driver-manager"></a>驅動程式管理員中的函式對應
驅動程式管理員支援採用字串引數的函式的兩個進入點。 未裝飾的函式 (**SQLDriverConnect**) 是 ANSI 格式的函式。 以 Unicode 格式以裝飾*W* (**SQLDriverConnectW**。)  
  
 ODBC 標頭檔也支援以裝飾的函式*A* (**SQLDriverConnectA**)，以提供混合式的 ANSI/Unicode 應用程式。 對呼叫**A**函式會實際呼叫的未裝飾的進入點 (**SQLDriverConnect**。)  
  
 如果應用程式編譯 _UNICODE **#define**，ODBC 標頭檔中會將對應的未裝飾的函式呼叫 (**SQLDriverConnect**) 的 Unicode 版本 (**SQLDriverConnectW**.)  
  
 驅動程式管理員會辨識 Unicode 驅動程式的驅動程式如果**SQLConnectW**支援的驅動程式。  
  
 如果驅動程式是 Unicode 驅動程式，驅動程式管理員呼叫函式，如下所示：  
  
-   傳遞直接傳遞給驅動程式沒有字串引數或參數的函式。  
  
-   將傳遞 Unicode 函式 (具有*W*後置詞) 直接透過驅動程式。  
  
-   將轉換的 ANSI 函式 (與*A*後置詞) 的 Unicode 函式 (與*W*後置詞) 將字串引數轉換成 Unicode 字元，並將 Unicode 函式傳遞至驅動程式。  
  
 如果驅動程式是 ANSI 驅動程式，驅動程式管理員呼叫函式，如下所示：  
  
-   將函式，而不需要字串引數或參數直接透過傳遞給驅動程式。  
  
-   轉換 Unicode 函式 (具有*W*後置詞) 為 ansi 函式呼叫，並將它傳遞給驅動程式。  
  
-   ANSI 函式會直接傳遞至驅動程式。  
  
 驅動程式管理員已啟用 Unicode 內部。 如此一來，最佳的效能，來取得 Unicode 應用程式使用 Unicode 驅動程式，因為驅動程式管理員只會將 Unicode 函式透過傳遞至驅動程式。 ANSI 應用程式使用時的 ANSI 驅動程式，則驅動程式管理員必須將字串轉換從 ANSI 為 Unicode 時處理某些函式，例如**SQLDriverConnect**。 在處理函式之後，驅動程式管理員必須再將轉換 Unicode 字串回 ANSI ANSI 驅動程式傳送函式之前。  
  
 應用程式不應該修改或驅動程式傳回 SQL_STILL_EXECUTING 或 SQL_NEED_DATA 時讀取其繫結的參數緩衝區。 驅動程式管理員會保留直到驅動程式傳回 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO 或 SQL_ERROR，ansi 繫結的緩衝區。 多執行緒應用程式不應該存取另一個執行緒執行 SQL 陳述式的任何繫結的參數值。 驅動程式管理員將資料從 Unicode 轉換成 ANSI 「 就地 」，另一個執行緒可能會看到這些緩衝區中的 ANSI 資料，但驅動程式仍在處理 SQL 陳述式。 Unicode 資料繫結至的 ANSI 驅動程式的應用程式必須連結到相同的位址的兩個不同的資料行。
