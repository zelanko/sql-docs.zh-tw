---
title: 桌面的診斷資料庫驅動程式 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], diagnostic information
- desktop database drivers [ODBC], diagnostic information
- ODBC desktop database drivers [ODBC], diagnostic information
- diagnostic information [ODBC], desktop database drivers
ms.assetid: 1c3740eb-62c6-4009-b4b2-570fcf5661e4
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3d5d82eb22f57fd033ea9250e1dd5532e72174e3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32904223"
---
# <a name="diagnostics-for-desktop-database-drivers"></a>桌面資料庫驅動程式的診斷功能
驅動程式會處理所有錯誤和警告不核取或部分核取驅動程式管理員。 驅動程式也會對應原生錯誤或傳回的資料來源，Sqlstate 的錯誤。 中所列每個函式*ODBC 程式設計人員參考*包含指定條件和訊息 「 診斷 」 一節。  
  
 應用程式呼叫**SQLGetDiagRec**擷取 SQLSTATE、 原生錯誤碼和診斷訊息。 呼叫**SQLGetDiagField** ，並指定欄位擷取個別的診斷欄位。 診斷的識別項的支援層級會列在下表中。  
  
|DiagIdentifiers|支援層級|  
|---------------------|-------------------|  
|SQL_DIA_DYNAMIC_FUNCTION|不支援|  
|SQL_DIAG_CLASS_ORIGIN|支援。 一律 「 ODBC 3.0"此驅動程式 3.0 版及更新版本。|  
|SQL_DIAG_COLUMN_NUMBER|Supported|  
|SQL_DIAG_CURSOR_ROW_COUNT|不支援|  
|為 SQL_DIAG_DYNAMIC_FUNCTION_CODE|不支援|  
|SQL_DIAG_MESSAGE_TEXT|Supported|  
|SQL_DIAG_NATIVE|Supported|  
|SQL_DIAG_NUMBER|Supported|  
|SQL_DIAG_RETURNCODE|支援，但實作由驅動程式管理員|  
|SQL_DIAG_ROW_COUNT|Supported|  
|SQL_DIAG_ROW_NUMBER|Supported|  
|SQL_DIAG_SERVER_NAME|不支援|  
|SQL_DIAG_SQLSTATE|Supported|  
|SQL_DIAG_SUBCLASS_ORIGIN|Supported|
