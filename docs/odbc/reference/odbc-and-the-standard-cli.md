---
title: ODBC 和標準 CLI |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], CLI
- CLI [ODBC]
- CLI [ODBC], about CLI
- call-level interface [ODBC]
- call-level interface [ODBC], about call-level interface
ms.assetid: 79b9c268-16ac-4b80-b451-f9dcd8c02ca4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 56dc0ac73c77cbbb77943d2e9ba308796b259dbb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305139"
---
# <a name="odbc-and-the-standard-cli"></a>ODBC 和標準 CLI
ODBC 符合與呼叫級介面 (CLI) 打交道的以下規範和標準。 (ODBC 功能是每個標準的超級集。  
  
-   打開組 CAE 規範"數據管理:SQL 調用級介面 (CLI)"  
  
-   ISO/IEC 9075-3:1995 (E) 呼叫級介面 (SQL/CLI)  
  
 由於這種對齊方式,以下情況為 true:  
  
-   寫入 Open Group 和 ISO CLI 規範的應用程式在使用 ODBC *3.x*標頭檔編譯並與 ODBC *3.x*庫連結時,以及透過 ODBC *3.x*驅動程式管理員存取驅動程式時,將使用 ODBC *3.x*驅動程式或符合標準的驅動程式。  
  
-   寫入 Open Group 和 ISO CLI 規範的驅動程式在使用 ODBC *3.x*標頭檔編譯並與 ODBC *3.x*庫連結時,以及當應用程式透過 ODBC *3.x*驅動程式管理員存取驅動程式時,它將與 ODBC *3.x*應用程式或符合標準的應用程式配合使用。 (關於詳細資訊,請參考[符合標準的應用程式和驅動程式](../../odbc/reference/develop-app/standards-compliant-applications-and-drivers.md)。  
  
 核心介面一致性級別包含 ISO CLI 中的所有功能以及開放組 CLI 中的所有非可選功能。 開放組 CLI 的可選功能顯示在更高的介面符合性級別中。 由於所有 ODBC *3.x*驅動程式都需要支援核心介面一致性級別的功能,因此如下所示:  
  
-   ODBC *3.x*驅動程式將支援符合標準的應用程式使用的所有功能。  
  
-   僅使用 ISO CLI 中的功能和開放組 CLI 的非可選功能的 ODBC *3.x*應用程式將與任何符合標準的驅動程式配合使用。  
  
 除了 ISO/IEC 和開放組 CLI 標準中包含的呼叫級介面規範外,ODBC 還實現了以下功能。 (其中一些功能存在於 ODBC *3.x*之前的 ODBC 版本中。  
  
-   以單函式呼叫取得多行  
  
-   繫結到參數陣列  
  
-   書籤支援,包括按書籤提取、可變長度書籤以及批量更新和刪除不連續行上的書籤操作  
  
-   資料列取向的繫結  
  
-   繫結位移  
  
-   支援批次處理 SQL 語句,無論是在儲存過程中,還是作為透過 SQLExecute 或**SQLExecDirect****SQLExecDirect**執行的 SQL 語句序列  
  
-   精確或近似游標行計數  
  
-   定位更新與移除操作以及按函式呼叫 **(SQLSetPos)** 批次處理更新與刪除  
  
-   目錄函數,無需支援資訊架構檢視,即可從資訊架構中提取資訊  
  
-   外部聯結、標量函數、日期時間文字、間隔文字和儲存過程的轉義序列  
  
-   代碼頁翻譯庫  
  
-   報告驅動程式的 ANSI 符合性層級與 SQL 支援  
  
-   依需要自動填充設定參數的描述  
  
-   增強的診斷及列和參數狀態陣列  
  
-   日期時間、間隔、數位/十進位和 64 位元整數應用程式緩衝區類型  
  
-   非同步執行  
  
-   儲存程序支援,包括轉義序列、輸出參數繫結機制及目錄函數  
  
-   連線增強功能,包括支援連接屬性和屬性瀏覽
