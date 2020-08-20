---
description: 驅動程式管理員中的函式對應
title: 驅動程式管理員中的函式對應 |Microsoft Docs
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
ms.openlocfilehash: 69434638dee25cdbad8428a1e09cb05a270f99de
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499842"
---
# <a name="function-mapping-in-the-driver-manager"></a>驅動程式管理員中的函式對應
驅動程式管理員針對採用字串引數的函數，支援兩個進入點。 未修飾的函式 (**SQLDriverConnect**) 是函數的 ANSI 格式。 Unicode 格式是以 *W* (**SQLDriverConnectW**來裝飾 )   
  
 ODBC 標頭檔也支援以 *A、* (**SQLDriverConnectA**) 裝飾的函式，以方便使用混合的 ANSI/Unicode 應用程式。 對函 **式的呼叫** 實際上會呼叫未修飾的進入點 (**SQLDriverConnect**。 )   
  
 如果使用 _UNICODE **#define**來編譯應用程式，ODBC 標頭檔將會將未裝飾函式呼叫 (**SQLDriverConnect**) 對應至 UNICODE 版本 (**SQLDriverConnectW**。 )   
  
 如果驅動程式支援 **SQLConnectW** ，驅動程式管理員會將驅動程式識別為 Unicode 驅動程式。  
  
 如果驅動程式是 Unicode 驅動程式，驅動程式管理員會進行函式呼叫，如下所示：  
  
-   將沒有字串引數或參數的函數直接傳遞至驅動程式。  
  
-   會將 Unicode 函式 (搭配 *W* 尾碼) 直接傳遞至驅動程式。  
  
-   將字串引數轉換成 Unicode 字元， *並將字串* 引數轉換成 unicode 字元，將 ANSI 函式 (與尾碼) 轉換成 unicode 函式)  (*，並將* unicode 函式傳遞至驅動程式。  
  
 如果驅動程式是 ANSI 驅動程式，驅動程式管理員會進行函式呼叫，如下所示：  
  
-   將沒有字串引數或參數的函數直接傳遞至驅動程式。  
  
-   將具有 *W* 尾碼的 Unicode 函式 (轉換) 至 ANSI 函式呼叫，並將其傳遞至驅動程式。  
  
-   將 ANSI 函數直接傳遞至驅動程式。  
  
 驅動程式管理員會在內部啟用 Unicode。 因此，使用 Unicode 驅動程式的 Unicode 應用程式會取得最佳效能，因為驅動程式管理員只會將 Unicode 函式傳遞至驅動程式。 當 ANSI 應用程式使用 ANSI 驅動程式時，驅動程式管理員必須在處理某些函數（例如 **SQLDriverConnect**）時，將字串從 ANSI 轉換成 Unicode。 處理函數之後，驅動程式管理員必須先將 Unicode 字串轉換回 ANSI，然後再將函數傳送給 ANSI 驅動程式。  
  
 當驅動程式傳回 SQL_STILL_EXECUTING 或 SQL_NEED_DATA 時，應用程式不應該修改或讀取其系結的參數緩衝區。 驅動程式管理員會離開系結至 ANSI 的緩衝區，直到驅動程式傳回 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO 或 SQL_ERROR 為止。 多執行緒應用程式不應該存取另一個執行緒正在執行 SQL 語句的任何系結參數值。 驅動程式管理員會將資料從 Unicode 轉換成 ANSI，而另一個執行緒可能會在這些緩衝區中看到 ANSI 資料，而驅動程式仍在處理 SQL 語句。 將 Unicode 資料系結至 ANSI 驅動程式的應用程式不能將兩個不同的資料行系結至相同的位址。
