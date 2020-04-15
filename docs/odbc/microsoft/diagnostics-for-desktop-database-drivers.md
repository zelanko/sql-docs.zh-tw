---
title: 桌面資料庫驅動程式的診斷 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303479"
---
# <a name="diagnostics-for-desktop-database-drivers"></a>桌面資料庫驅動程式的診斷
驅動程式管理員未檢查或部分檢查的所有錯誤和警告都由驅動程式處理。 該驅動程式還將本機錯誤或數據源返回的錯誤對應到 SQLSTAT。 *ODBC 程式師參考*中列出的每個函數都包含一個"診斷"部分,用於指定條件和消息。  
  
 應用程式呼叫**SQLGetDiagRec**來檢索 SQLSTATE、本機錯誤代碼和診斷消息。 呼叫**SQLGetDiagField**並指定該欄位將檢索各個診斷欄位。 下表列出了診斷標識符的支持級別。  
  
|診斷識別碼|支援層級|  
|---------------------|-------------------|  
|SQL_DIA_DYNAMIC_FUNCTION|不支援|  
|SQL_DIAG_CLASS_ORIGIN|支援。 對於此驅動程式的版本 3.0 和更高版本,始終為"ODBC 3.0"。|  
|SQL_DIAG_COLUMN_NUMBER|支援|  
|SQL_DIAG_CURSOR_ROW_COUNT|不支援|  
|SQL_DIAG_DYNAMIC_FUNCTION_CODE|不支援|  
|SQL_DIAG_MESSAGE_TEXT|支援|  
|SQL_DIAG_NATIVE|支援|  
|SQL_DIAG_NUMBER|支援|  
|SQL_DIAG_RETURNCODE|驅動程式管理員支援但實施|  
|SQL_DIAG_ROW_COUNT|支援|  
|SQL_DIAG_ROW_NUMBER|支援|  
|SQL_DIAG_SERVER_NAME|不支援|  
|SQL_DIAG_SQLSTATE|支援|  
|SQL_DIAG_SUBCLASS_ORIGIN|支援|
