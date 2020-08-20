---
description: 符合標準的應用程式和驅動程式
title: 符合標準的應用程式和驅動程式 |Microsoft Docs
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
ms.openlocfilehash: e6733afa5281f86d8dd425e6157832ee0680d34b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476380"
---
# <a name="standards-compliant-applications-and-drivers"></a>符合標準的應用程式和驅動程式
符合標準規範的應用程式或驅動程式，就是符合 Open Group CAE 規格「資料管理： SQL 呼叫層級介面 (CLI) 」，以及 ISO/IEC 9075-3:1995 (E) 呼叫層級介面 (SQL/CLI) 。  
  
 ODBC *3.x* 可確保下列功能：  
  
-   寫入 Open 群組和 ISO CLI 規格的應用程式將會 *使用 odbc 3.x 的驅動程式* 或符合標準的驅動程式（使用 odbc 3.x 標頭檔進行編譯，並連結 *到 odbc 3.x* *程式庫）* ，以及透過 odbc *3.x 驅動程式* 管理員取得驅動程式的存取權。  
  
-   寫入開放式群組和 ISO CLI 規格的驅動程式，將會使用 odbc 3.x*標頭檔編譯的 odbc* *3.x 應用程式*或符合標準的應用程式，並*與 odbc 3.x 程式庫連結*，以及當應用程式透過 odbc *3.x 驅動程式*管理員取得驅動程式的存取權時。  
  
 符合標準的應用程式和驅動程式會使用 ODBC_STD 編譯旗標進行編譯。  
  
 符合標準的應用程式會展示下列行為：  
  
-   如果符合標準的應用程式呼叫 (**SQLAllocEnv** ，就會發生這種情況，因為 **SQLAllocEnv** 是開啟群組和 ISO CLI 中的有效函式) ，所以在編譯時期，呼叫會對應至 **SQLAllocHandleStd** 。 因此，在執行時間，應用程式會呼叫 **SQLAllocHandleStd**。 在處理此呼叫的過程中，驅動程式管理員會將 SQL_ATTR_ODBC_VERSION 環境屬性設定為 SQL_OV_ODBC3。 對**SQLAllocHandleStd**的呼叫相當於呼叫*HandleType*為 SQL_HANDLE_ENV 的**SQLAllocHandle** ，以及對**SQLSetEnvAttr**的呼叫，以將 SQL_ATTR_ODBC_VERSION 設定為 SQL_OV_ODBC3。  
  
-   如果符合標準的應用程式呼叫 (**SQLBindParam** ，就會發生這種情況，因為 **SQLBindParam** 是 OPEN 群組和 ISO CLI) 中的有效功能， *所以 ODBC 3.x 驅動程式* 管理員會將呼叫對應至 **SQLBindParameter**中的對等呼叫。  (請參閱附錄 G：適用于回溯相容性的驅動程式指導方針中的 [SQLBindParam 對應](../../../odbc/reference/appendixes/sqlbindparam-mapping.md) 。 )   
  
-   為了與 ISO CLI 一致 *，ODBC 3.x* 標頭檔包含在 **SQLGetInfo**呼叫中使用之資訊類型的別名。 符合標準的應用程式可以使用這些別名，而不是 *ODBC 3.x* 資訊類型。 如需詳細資訊，請參閱下一個主題的 [標頭檔](../../../odbc/reference/develop-app/header-files.md)。  
  
-   符合標準的應用程式必須確認它所支援的所有功能都可在它將使用的驅動程式中受到支援。 將 SQL_ATTR_CURSOR_SCROLLABLE 語句屬性設定為 SQL_SCROLLABLE，並將 SQL_ATTR_CURSOR_SENSITIVITY 語句屬性設定為 SQL_INSENSITIVE 或 SQL_SENSITIVE，這項功能可做為標準中的選擇性功能，但不會包含*在 odbc 3.x*的核心層級中，因此可能不會受到*所有 odbc 3.x*驅動程式的支援。 如果符合標準的應用程式使用這些功能，則應該確認它要使用的驅動程式是否支援它們。
