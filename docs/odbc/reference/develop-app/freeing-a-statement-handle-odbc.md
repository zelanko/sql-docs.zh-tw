---
title: 釋放語句句柄 ODBC |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- statement handles [ODBC]
- handles [ODBC], statement
- freeing statement handles [ODBC]
ms.assetid: ee18e2f1-2690-4cc1-9e5c-e20244e5d480
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 01e4cb46edf1b1a0f1c6dfaa0273c1dd5b392686
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305613"
---
# <a name="freeing-a-statement-handle-odbc"></a>釋放陳述式控制代碼 ODBC
如前所述,重用語句比刪除語句和分配新語句更有效。 在語句上執行新的 SQL 語句之前,應用程式應確保當前語句設置是合適的。 這些包括陳述式屬性、參數繫結，以及結果集繫結。 通常,舊 SQL 語句的參數和結果集需要取消綁定(使用SQL_RESET_PARAMS和SQL_UNBIND選項調用**SQLFreeStmt),** 並恢復新的 SQL 語句。  
  
 當應用程式完成使用 語句后,它將調用**SQLFreeHandle**來釋放該語句。 釋放語句后,在調用 ODBC 函數時使用語句的句柄是應用程式程式設計錯誤;這樣做有未定義,但可能是致命的後果。  
  
 調用**SQLFreeHandle**時,驅動程式將釋放用於存儲有關語句的資訊的結構。  
  
 **SQLDISCONNECT**會自動釋放連接上的所有語句。
