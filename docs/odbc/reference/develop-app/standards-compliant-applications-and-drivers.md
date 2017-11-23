---
title: "符合標準的應用程式和驅動程式 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- standards-compliant applications and drivers [ODBC]
- ODBC drivers [ODBC], standards-compliant
- application features are standards-compliant [ODBC]
ms.assetid: a1145c4c-3094-4f3f-8cc2-e6bb1a930ab1
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c62e19d2d7c2c856b358649955a5b1540a802a12
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="standards-compliant-applications-and-drivers"></a>符合標準的應用程式和驅動程式
符合標準的應用程式或驅動程式是一個符合開放式群組 CAE 規格 」 的資料管理:: SQL 呼叫層級介面 (CLI)，"和 ISO/IEC 9075-3:1995 (E) 呼叫層級介面 (SQL/CLI)。  
  
 ODBC 3*.x*保證下列功能：  
  
-   Open Group 和 ISO CLI 規格所撰寫的應用程式將會使用 ODBC 3*.x*驅動程式或標準相容的驅動程式編譯時與 ODBC 3*.x*標頭檔，並與連結ODBC 3*.x*程式庫，以及當它所獲得的存取權的驅動程式透過 ODBC 3*.x*驅動程式管理員。  
  
-   寫入的 Open Group 和 ISO CLI 規格的驅動程式將會使用 ODBC 3*.x*應用程式或標準相容的應用程式編譯時與 ODBC 3*.x*標頭檔和連結ODBC 3*.x*文件庫和應用程式時取得存取權的驅動程式透過 ODBC 3*.x*驅動程式管理員。  
  
 符合標準的應用程式和驅動程式會編譯 ODBC_STD 編譯旗標。  
  
 符合標準的應用程式表現下列行為：  
  
-   如果符合標準的應用程式呼叫**SQLAllocEnv** (這可能是因為**SQLAllocEnv**是有效的函式中的 Open Group 和 ISO CLI)，在呼叫對應至**SQLAllocHandleStd**在編譯時間。 如此一來，在執行階段，應用程式呼叫**SQLAllocHandleStd**。 處理此呼叫的期間，驅動程式管理員會設定為 SQL_OV_ODBC3 SQL_ATTR_ODBC_VERSION 環境屬性。 呼叫**SQLAllocHandleStd**相當於呼叫**SQLAllocHandle**與*HandleType* SQL_HANDLE_ENV 和呼叫**SQLSetEnvAttr** SQL_ATTR_ODBC_VERSION 設定為 SQL_OV_ODBC3。  
  
-   如果符合標準的應用程式呼叫**SQLBindParam** (這可能是因為**SQLBindParam**是有效的函式中的 Open Group 和 ISO CLI)，ODBC 3*.x*驅動程式管理員會將對應的呼叫中的對等呼叫**SQLBindParameter**。 (請參閱[SQLBindParam 對應](../../../odbc/reference/appendixes/sqlbindparam-mapping.md)附錄 g： 驅動程式的指導方針回溯相容性中。)  
  
-   若要配合 ISO CLI，而 ODBC 3*.x*標頭檔包含對呼叫中使用的資訊類型的別名**SQLGetInfo**。 符合標準的應用程式可以使用這些別名，而不是 ODBC 3*.x*資訊類型。 如需詳細資訊，請參閱下一個主題[標頭檔](../../../odbc/reference/develop-app/header-files.md)。  
  
-   符合標準的應用程式必須確認它所支援的所有功能都支援將使用驅動程式中。 將 SQL_ATTR_CURSOR_SCROLLABLE 陳述式屬性設定為 SQL_SCROLLABLE 和設定 SQL_INSENSITIVE 或 SQL_SENSITIVE SQL_ATTR_CURSOR_SENSITIVITY 陳述式屬性是可做為標準中的選用功能的功能但不是包含在 ODBC 3*.x*核心層級，因此可能不支援所有 ODBC 3*.x*驅動程式。 如果符合標準的應用程式使用這些功能，它應該確認它可以搭配此驅動程式支援它們。
