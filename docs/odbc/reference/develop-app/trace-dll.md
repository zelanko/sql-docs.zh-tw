---
title: 追蹤 DLL |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- trace DLLs [ODBC]
- tracing options [ODBC], trace DLLs
ms.assetid: 5ab99bd3-cdc3-4e2c-8827-932d1fcb6e00
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d7a99f6c2960600d62a789471f68c1f5da89ae8c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47647836"
---
# <a name="trace-dll"></a>追蹤 DLL
執行追蹤的 DLL 是其中一個 ODBC 核心元件。 目前提供跖秷 DLL 在 Windows SDK 的 ODBC 元件 DLL，並已在追蹤先前包含 Microsoft Data Access Components (MDAC) SDK。 因此，登錄項目、 介面和追蹤 DLL 的範例程式碼都可用。 被追蹤 ODBC 使用者或第三方廠商所產生的 DLL，就可以取代此 DLL。 自訂追蹤 DLL 應該具備不同原始範例追蹤 DLL 的名稱。 追蹤 Dll 必須安裝在系統目錄中，或他們將無法載入。 連接字串不會傳遞至追蹤 DLL 透過驅動程式管理員。  
  
 追蹤 DLL 追蹤輸入引數 」、 「 輸出引數 」、 「 延後的引數 」、 「 傳回碼和 「 Sqlstate。 當啟用追蹤時，驅動程式管理員會呼叫兩個點的追蹤 DLL: （在之前引數的驗證） 的函式進入時，一次，而且一次函式會傳回之前。  
  
 當應用程式呼叫的函式時，驅動程式管理員會追蹤驅動程式中呼叫函式，或處理本身的呼叫之前的 DLL 中呼叫追蹤函式。 每個 ODBC 函式具有對應的追蹤函式 (前面加上*追蹤*) 與 ODBC 函式，除了名稱之外完全相同。 追蹤函式呼叫時，追蹤 DLL 擷取輸入引數，並傳回傳回碼。 因為追蹤 DLL 會呼叫之前，驅動程式管理員會驗證引數，會追蹤無效的函式呼叫，因此會記錄狀態轉換錯誤和無效的引數。  
  
 在呼叫之後追蹤功能追蹤 DLL 中，驅動程式管理員會呼叫驅動程式中的 ODBC 函式。 然後它會呼叫**TraceReturn**追蹤 DLL 中。 此函數會採用兩個引數： 追蹤函式的追蹤 DLL 所傳回的值和傳回碼傳回的驅動程式的 ODBC 函式驅動程式管理員 （或處理函式傳回由驅動程式管理員本身的值）。 此函數會使用追蹤函式傳回的值來操作擷取輸入引數的值。 它寫入至記錄檔傳回 ODBC 函數的程式碼 （或如果已啟用它，以動態方式顯示）。 它會輸出引數指標取值，並記錄的輸出引數值。
