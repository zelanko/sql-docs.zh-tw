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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8e1f9dc57415ad9865ca1b2ad02487b62a93f18f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "81298068"
---
# <a name="trace-dll"></a>追蹤 DLL
執行追蹤的 DLL 是其中一個 ODBC core 元件。 追蹤 DLL 目前在 Windows SDK 的 ODBC 元件中提供為範例 DLL，先前已包含 Microsoft Data Access Components （MDAC） SDK。 因此，可以使用追蹤 DLL 的登錄專案、介面和範例程式碼。 這個 DLL 可以由 ODBC 使用者或協力廠商所產生的追蹤 DLL 來取代。 自訂追蹤 DLL 的名稱應該與原始的範例追蹤 DLL 不同。 追蹤 Dll 必須安裝在系統目錄中，否則將無法載入。 驅動程式管理員不會將連接字串傳遞到追蹤 DLL。  
  
 追蹤 DLL 會追蹤輸入引數、輸出引數、延遲引數、傳回碼和 SQLSTATEs。 啟用追蹤時，驅動程式管理員會在兩個點呼叫追蹤 DLL：一次在函式進入後（引數驗證之前），然後在函式傳回之前。  
  
 當應用程式呼叫函式時，驅動程式管理員會在呼叫驅動程式中的函式或處理呼叫本身之前，先呼叫追蹤 DLL 中的追蹤函數。 每個 ODBC 函式都有對應的追蹤函式（前面加上*trace*），與 ODBC 函數相同，但名稱除外。 呼叫 trace 函數時，追蹤 DLL 會捕捉輸入引數，並傳回傳回碼。 由於在驅動程式管理員驗證引數之前會呼叫追蹤 DLL，因此會追蹤不正確函式呼叫，因此會記錄狀態轉換錯誤和不正確引數。  
  
 在追蹤 DLL 中呼叫 trace 函數之後，驅動程式管理員會呼叫驅動程式中的 ODBC 函數。 然後，它會呼叫追蹤 DLL 中的**TraceReturn** 。 此函式會採用兩個引數：追蹤 DLL 針對 trace 函式所傳回的值，以及驅動程式傳回給 ODBC 函式之驅動程式管理員的傳回碼（如果處理函式，則為驅動程式管理員本身所傳回的值）。 函式會使用針對 trace 函數傳回的值，來操作已捕捉的輸入引數值。 它會將 ODBC 函式傳回的程式碼寫入記錄檔（如果已啟用，則會動態顯示）。 它會對輸出引數指標取值，並記錄輸出引數的值。
