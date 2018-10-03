---
title: 診斷桌面資料庫驅動程式 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d6c21af2ef3f47c05aacf4b47673ab42a170f506
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47709626"
---
# <a name="diagnostics-for-desktop-database-drivers"></a>桌面資料庫驅動程式的診斷
驅動程式會處理所有錯誤和警告不核取或部分核取驅動程式管理員。 驅動程式也會對應原生錯誤或傳回的資料來源，Sqlstate 的錯誤。 中所列每個函式*ODBC 程式設計人員參考*包含會指定條件和訊息 「 診斷 」 一節。  
  
 應用程式會呼叫**SQLGetDiagRec**擷取 SQLSTATE、 原生錯誤碼，以及診斷訊息。 呼叫**SQLGetDiagField** ，並指定欄位擷取個別的診斷欄位。 支援的層級的診斷識別碼會列在下表中。  
  
|DiagIdentifiers|支援層級|  
|---------------------|-------------------|  
|SQL_DIA_DYNAMIC_FUNCTION|不支援|  
|SQL_DIAG_CLASS_ORIGIN|支援。 一律"ODBC 3.0"此驅動程式 3.0 版及更新版本。|  
|SQL_DIAG_COLUMN_NUMBER|支援|  
|SQL_DIAG_CURSOR_ROW_COUNT|不支援|  
|SQL_DIAG_DYNAMIC_FUNCTION_CODE|不支援|  
|SQL_DIAG_MESSAGE_TEXT|支援|  
|SQL_DIAG_NATIVE|支援|  
|SQL_DIAG_NUMBER|支援|  
|SQL_DIAG_RETURNCODE|支援，但實作由驅動程式管理員|  
|SQL_DIAG_ROW_COUNT|支援|  
|SQL_DIAG_ROW_NUMBER|支援|  
|SQL_DIAG_SERVER_NAME|不支援|  
|SQL_DIAG_SQLSTATE|支援|  
|SQL_DIAG_SUBCLASS_ORIGIN|支援|
