---
title: "追蹤 DLL |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- trace DLLs [ODBC]
- tracing options [ODBC], trace DLLs
ms.assetid: 5ab99bd3-cdc3-4e2c-8827-932d1fcb6e00
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 22bbb28f42f7bd3c1ec32e01c3451944315861a0
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="trace-dll"></a>追蹤 DLL
執行追蹤的 DLL 是一個 ODBC 核心元件。 追蹤目前提供跖秷 DLL 中的 Windows SDK，ODBC 元件 DLL，並已收錄 Microsoft Data Access Components (MDAC) SDK。 因此，登錄項目、 介面和追蹤 DLL 的範例程式碼使用。 這個 DLL 可追蹤 ODBC 使用者或協力廠商所產生的 DLL 所取代。 自訂追蹤 DLL 應該具備不同原始範例追蹤 DLL 的名稱。 追蹤 Dll 必須安裝在系統目錄中，或它們將無法載入。 連接字串不會傳遞至追蹤 DLL 由驅動程式管理員。  
  
 追蹤 DLL 追蹤輸入引數、 輸出引數、 延後的引數、 傳回碼和 Sqlstate。 當啟用追蹤時，驅動程式管理員會呼叫兩個點的追蹤 DLL： 一次 （在之前的驗證引數） 的函式進入時，一次只函式會傳回之前。  
  
 當應用程式呼叫的函式時，驅動程式管理員會追蹤驅動程式中呼叫函式，或處理呼叫本身之前的 DLL 中呼叫追蹤函式。 每個 ODBC 函式具有對應的追蹤函式 (前面加上*追蹤*) 與 ODBC 函數，除了名稱之外完全相同。 追蹤函式呼叫時，追蹤 DLL 擷取輸入引數，並傳回傳回碼。 由於追蹤 DLL 之前驅動程式管理員會驗證引數呼叫，會追蹤無效的函式呼叫，以便記錄狀態轉換錯誤和無效的引數。  
  
 在呼叫之後追蹤函式中追蹤 DLL，驅動程式管理員會呼叫驅動程式中的 ODBC 函數。 然後它會呼叫**TraceReturn**追蹤 DLL 中。 此函數會採用兩個引數： 追蹤函式的追蹤 DLL 所傳回的值和驅動程式傳回給驅動程式管理員的 ODBC 函數的傳回碼 （或在處理函式傳回的驅動程式管理員本身的值）。 此函數會使用追蹤函式的傳回值，管理擷取輸入引數的值。 它會寫入至記錄檔的 ODBC 函數傳回的程式碼 （或如果已啟用它，以動態方式顯示）。 它對輸出引數指標取值，並記錄的輸出引數值。

