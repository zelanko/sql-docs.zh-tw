---
title: "桌面的診斷資料庫驅動程式 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], diagnostic information
- desktop database drivers [ODBC], diagnostic information
- ODBC desktop database drivers [ODBC], diagnostic information
- diagnostic information [ODBC], desktop database drivers
ms.assetid: 1c3740eb-62c6-4009-b4b2-570fcf5661e4
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5440d7cb38dfeef678a9b665397b789bf506be72
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="diagnostics-for-desktop-database-drivers"></a>桌面資料庫驅動程式的診斷功能
驅動程式會處理所有錯誤和警告不核取或部分核取驅動程式管理員。 驅動程式也會對應原生錯誤或傳回的資料來源，Sqlstate 的錯誤。 中所列每個函式*ODBC 程式設計人員參考*包含指定條件和訊息 「 診斷 」 一節。  
  
 應用程式呼叫**SQLGetDiagRec**擷取 SQLSTATE、 原生錯誤碼和診斷訊息。 呼叫**SQLGetDiagField** ，並指定欄位擷取個別的診斷欄位。 診斷的識別項的支援層級會列在下表中。  
  
|DiagIdentifiers|支援層級|  
|---------------------|-------------------|  
|SQL_DIA_DYNAMIC_FUNCTION|不支援|  
|SQL_DIAG_CLASS_ORIGIN|支援。 一律 「 ODBC 3.0"此驅動程式 3.0 版及更新版本。|  
|SQL_DIAG_COLUMN_NUMBER|支援|  
|SQL_DIAG_CURSOR_ROW_COUNT|不支援|  
|為 SQL_DIAG_DYNAMIC_FUNCTION_CODE|不支援|  
|SQL_DIAG_MESSAGE_TEXT|支援|  
|SQL_DIAG_NATIVE|支援|  
|SQL_DIAG_NUMBER|支援|  
|SQL_DIAG_RETURNCODE|支援，但實作由驅動程式管理員|  
|SQL_DIAG_ROW_COUNT|支援|  
|SQL_DIAG_ROW_NUMBER|支援|  
|SQL_DIAG_SERVER_NAME|不支援|  
|SQL_DIAG_SQLSTATE|支援|  
|SQL_DIAG_SUBCLASS_ORIGIN|支援|
