---
title: 符合標準的應用程式和驅動程式 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- standards-compliant applications and drivers [ODBC]
- ODBC drivers [ODBC], standards-compliant
- application features are standards-compliant [ODBC]
ms.assetid: a1145c4c-3094-4f3f-8cc2-e6bb1a930ab1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4b4daf2e777b20b1b84c090757d0d84796a4cae1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299715"
---
# <a name="standards-compliant-applications-and-drivers"></a>符合標準的應用程式和驅動程式
符合標準的應用程式或驅動程式符合開放組 CAE 規範「數據管理:SQL 調用級介面 (CLI)」和 ISO/IEC 9075-3:1995 (E) 呼叫級介面 (SQL/CLI)。  
  
 ODBC *3.x*保證具有以下功能:  
  
-   寫入 Open Group 和 ISO CLI 規範的應用程式在使用 ODBC *3.x*標頭檔編譯並與 ODBC *3.x*庫連結時,以及透過 ODBC *3.x*驅動程式管理員存取驅動程式時,將使用 ODBC *3.x*驅動程式或符合標準的驅動程式。  
  
-   寫入 Open Group 和 ISO CLI 規範的驅動程式在使用 ODBC *3.x*標頭檔編譯並與 ODBC *3.x*庫連結時,以及當應用程式透過 ODBC *3.x*驅動程式管理員存取驅動程式時,它將與 ODBC *3.x*應用程式或符合標準的應用程式配合使用。  
  
 符合標準的應用程式和驅動程式使用ODBC_STD編譯標誌進行編譯。  
  
 符合標準的應用程式表現出以下行為:  
  
-   如果符合標準的應用程式調用**SQLAllocEnv(** 這可能是因為**SQLAllocEnv**是 Open 組和 ISO CLI 中的有效函數,則調用將在編譯時映射到**SQLAlloc HandleStd。** 因此,在執行時,應用程式呼叫**SQLAllocHandleStd**。 在處理此調用的過程中,驅動程式管理器將SQL_ATTR_ODBC_VERSION環境屬性設置為SQL_OV_ODBC3。 對**SQLAllocHandleStd**的調用等效於對**SQLAllocHandle**的調用,該調用具有SQL_HANDLE_ENV*的句柄類型*,以及對**SQLSetEnv Attr**的調用,以將SQL_ATTR_ODBC_VERSION設置為SQL_OV_ODBC3。  
  
-   如果符合標準的應用程式呼叫**SQLBindParam(** 這可能是因為**SQLBindParam**是開放組和 ISO CLI 中的有效函數),則 ODBC *3.x*驅動程式管理器將調用映射到**SQLBind 參數**中的等效調用。 (請參閱附錄 G 中的[SQLBindParam 映射](../../../odbc/reference/appendixes/sqlbindparam-mapping.md):向後相容性的驅動程式指南。  
  
-   要與 ISO CLI 保持一致,ODBC *3.x*標頭檔包含調用**SQLGetInfo**中使用的資訊類型的別名。 符合標準的應用程式可以使用這些別名而不是 ODBC *3.x*資訊類型。 有關詳細資訊,請參閱下一個主題[「標題檔](../../../odbc/reference/develop-app/header-files.md)」。  
  
-   符合標準的應用程式必須驗證它支援的所有功能是否在其要使用的驅動程式中支援。 將SQL_ATTR_CURSOR_SCROLLABLE語句屬性設置為SQL_SCROLLABLE並將SQL_ATTR_CURSOR_SENSITIVITY語句屬性設置為SQL_INSENSITIVE或SQL_SENSITIVE是標準中可選功能,但不包括在 ODBC *3.x* Core 級別,因此可能不受所有 ODBC *3.x*驅動程式支援的功能。 如果符合標準的應用程式使用這些功能,它應驗證驅動程式是否將使用它們。
