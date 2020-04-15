---
title: 跟蹤 DLL |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298068"
---
# <a name="trace-dll"></a>追蹤 DLL
執行追蹤的 DLL 是 ODBC 核心元件之一。 追蹤 DLL 目前作為範例 DLL 在 Windows SDK 的 ODBC 元件中提供,並且以前包括 Microsoft 資料存取元件 (MDAC) SDK。 因此,跟蹤 DLL 的註冊表項、介面和示例代碼可用。 此 DLL 可以取代為由 ODBC 使用者或第三方供應商生成的追蹤 DLL。 應為自訂追蹤 DLL 指定與原始範例追蹤 DLL 不同的名稱。 跟蹤 DLL 必須安裝在系統目錄中,否則將無法載入。 驅動程式管理員不會將連接字串傳遞到追蹤 DLL。  
  
 跟蹤 DLL 追蹤輸入參數、輸出參數、延遲參數、返回代碼和 SQLSTAT。 啟用追蹤後,Driver Manager 將在兩個點調用追蹤 DLL:一次在函數條目(參數驗證之前),另一次在函數返回之前調用。  
  
 當應用程式呼叫函數時,驅動程式管理員在調用驅動程式中的函數或處理呼叫本身之前,在追蹤 DLL 中呼叫追蹤函數。 每個 ODBC 函數都有一個相應的跟蹤函數(以*跟蹤*為預置),該函數與 ODBC 函數相同,但名稱除外。 呼叫追蹤函數時,追蹤 DLL 捕獲輸入參數並返回返回代碼。 由於在驅動程式管理器驗證參數之前調用了跟蹤 DLL,因此將追蹤無效的函數調用,因此記錄狀態轉換錯誤和無效參數。  
  
 在追蹤 DLL 中呼叫追蹤函數後,驅動程式管理器在驅動程式中呼叫 ODBC 函數。 在追蹤 DLL 中呼叫**追蹤傳回**。 此函數採用兩個參數:跟蹤函數的跟蹤 DLL 返回的值,以及驅動程式返回到 ODBC 函數的驅動程式管理員的返回代碼(或者驅動程式管理員本身處理該函數時返回的值)。 函數使用為跟蹤函數返回的值來操作捕獲的輸入參數值。 它將為 ODBC 函數傳回的代碼寫入紀錄檔(如果啟用,則動態顯示)。 它取消引用輸出參數指標並記錄輸出參數值。
