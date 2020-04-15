---
title: 連線選項 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection options [ODBC]
- ODBC driver for Oracle [ODBC], connection options
- custom connection options [ODBC]
ms.assetid: abfdc133-cb33-435f-a467-fbe15444f687
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 25cfe2a897b0c312f91cd0c1e41ad6fa11725ab8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81281308"
---
# <a name="connect-options"></a>連線選項
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 而是使用 Oracle 提供的 ODBC 驅動程式。  
  
 這些選項允許自定義應用程式中的資料庫連接。  
  
|連線選項|注意|  
|--------------------|-----------|  
|SQL_AUTOCOMMIT|如果選擇SQL_AUTOCOMMIT_OFF,則應用程式必須顯式提交或回滾[SQLTransact 的](../../odbc/microsoft/core-level-api-functions-odbc-driver-for-oracle.md)事務。|  
|SQL_ODBC_CURSORS|此連接屬性在驅動程式管理器中實現。|  
|SQL_OPT_TRACE|此連接屬性在驅動程式管理器中實現。|  
|SQL_OPT_TRACEFILE|此連接屬性在驅動程式管理器中實現。|  
|SQL_TRANSLATE_DLL|返回錯誤:「驅動程序無法。|  
|SQL_TRANSLATE_OPTION|傳遞給翻譯 .dll 的 32 位值。|  
|SQL_TXN_ISOLATION|驅動程式只允許SQL_TXN_READ_COMMITTED。<br /><br /> 不支援以下 vParams:<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
|SQL_ATTR_ENLIST_IN_DTC|此 ODBC 3.0 連接屬性允許您在 Microsoft 元件服務(如果使用 Windows NT)協調的分散式事務中使用 Oracle 的 ODBC 驅動程式。 它提供介面指標*pI交易*到事務作為*vParam*參數。|  
|SQL_ATTR_CONNECTION_DEAD|此唯讀 ODBC 3.5 連接屬性允許您確定與 Oracle 伺服器的連線是否失敗。 只獲取;無法設置。|
