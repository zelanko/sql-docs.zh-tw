---
description: 追蹤 DLL
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
ms.openlocfilehash: 1791b72b5f7e836fba05275f87bd57948a273775
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487501"
---
# <a name="trace-dll"></a>追蹤 DLL
執行追蹤的 DLL 是其中一個 ODBC 核心元件。 追蹤 DLL 目前在 Windows SDK 的 ODBC 元件中提供為範例 DLL，先前已包含 Microsoft Data Access Components (MDAC) SDK。 因此，可以使用追蹤 DLL 的登錄專案、介面和程式碼範例。 此 DLL 可由 ODBC 使用者或協力廠商所產生的追蹤 DLL 來取代。 自訂追蹤 DLL 的名稱應與原始的範例追蹤 DLL 不同。 追蹤 Dll 必須安裝在系統目錄中，否則將無法載入。 驅動程式管理員不會將連接字串傳遞至追蹤 DLL。  
  
 追蹤 DLL 會追蹤輸入引數、輸出引數、延遲的引數、傳回碼和 SQLSTATEs。 啟用追蹤時，驅動程式管理員會在兩個點呼叫追蹤 DLL：一次是在引數驗證之前的函式輸入 (，) 在函式傳回之前。  
  
 當應用程式呼叫函式時，驅動程式管理員會在呼叫驅動程式中的函式或處理呼叫本身之前，在追蹤 DLL 中呼叫追蹤函數。 每個 ODBC 函數都有對應的追蹤函式 (前面加上 *追蹤*) ，與 ODBC 函式相同，但名稱除外。 呼叫 trace 函數時，追蹤 DLL 會捕捉輸入引數，並傳回傳回碼。 由於追蹤 DLL 是在驅動程式管理員驗證引數之前呼叫，因此會追蹤不正確函式呼叫，因此會記錄狀態轉換錯誤和不正確引數。  
  
 在追蹤 DLL 中呼叫追蹤函數之後，驅動程式管理員會在驅動程式中呼叫 ODBC 函數。 然後，它會在追蹤 DLL 中呼叫 **TraceReturn** 。 此函式會採用兩個引數：追蹤函式的追蹤 DLL 所傳回的值，以及由驅動程式傳回的傳回碼到 ODBC 函數的驅動程式管理員 (或由驅動程式管理員在處理函式) 時所傳回的值。 函數會使用針對追蹤函式所傳回的值來操作已捕捉的輸入引數值。 它會將 ODBC 函數所傳回的程式碼寫入至記錄檔 (或動態顯示（如果已啟用) ）。 它會對輸出引數指標進行取值，並記錄輸出引數值。
