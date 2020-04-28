---
title: 桌面資料庫驅動程式的診斷 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], diagnostic information
- desktop database drivers [ODBC], diagnostic information
- ODBC desktop database drivers [ODBC], diagnostic information
- diagnostic information [ODBC], desktop database drivers
ms.assetid: 1c3740eb-62c6-4009-b4b2-570fcf5661e4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 99603c047e77d3cd3e077c1b07c2192eeb65f93c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303479"
---
# <a name="diagnostics-for-desktop-database-drivers"></a>桌面資料庫驅動程式的診斷
驅動程式管理員未檢查或部分檢查的所有錯誤和警告，都是由驅動程式處理。 驅動程式也會將原生錯誤或資料來源所傳回的錯誤對應至 SQLSTATEs。 ODBC 程式設計*人員參考*中列出的每個函式都包含指定條件和訊息的「診斷」區段。  
  
 應用程式會呼叫**SQLGetDiagRec**來取出 SQLSTATE、原生錯誤碼和診斷訊息。 呼叫**SQLGetDiagField**並指定欄位，會抓取個別的診斷欄位。 下表列出診斷識別碼的支援層級。  
  
|DiagIdentifiers|支援層級|  
|---------------------|-------------------|  
|SQL_DIA_DYNAMIC_FUNCTION|不受支援|  
|SQL_DIAG_CLASS_ORIGIN|支援。 此驅動程式的版本3.0 及更新版本一律為 "ODBC 3.0"。|  
|SQL_DIAG_COLUMN_NUMBER|支援|  
|SQL_DIAG_CURSOR_ROW_COUNT|不受支援|  
|SQL_DIAG_DYNAMIC_FUNCTION_CODE|不受支援|  
|SQL_DIAG_MESSAGE_TEXT|支援|  
|SQL_DIAG_NATIVE|支援|  
|SQL_DIAG_NUMBER|支援|  
|SQL_DIAG_RETURNCODE|支援但由驅動程式管理員執行|  
|SQL_DIAG_ROW_COUNT|支援|  
|SQL_DIAG_ROW_NUMBER|支援|  
|SQL_DIAG_SERVER_NAME|不受支援|  
|SQL_DIAG_SQLSTATE|支援|  
|SQL_DIAG_SUBCLASS_ORIGIN|支援|
