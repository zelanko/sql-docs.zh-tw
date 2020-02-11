---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4980cfe64a5a8e8404c6b5b0bdc8b1aba484f0c0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68107336"
---
# <a name="standards-compliant-applications-and-drivers"></a>符合標準的應用程式和驅動程式
符合標準的應用程式或驅動程式是符合開放式群組 CAE 規格「資料管理： SQL 呼叫層級介面（CLI）」，以及 ISO/IEC 9075-3:1995 （E）呼叫層級介面（SQL/CLI）的其中一個。  
  
 ODBC *3.x*可保證下列功能：  
  
-   寫入 Open 群組和 ISO CLI 規格的應用程式，會*使用 odbc 3.x 驅動程式*或符合標準的驅動程式（當它使用 odbc 3.x 標頭檔進行編譯並*與 odbc 3.x* *程式庫一起*使用時），以及當它透過 odbc *3.x 驅動程式*管理員取得驅動程式的存取權時。  
  
-   寫入開放式群組和 ISO CLI 規格的驅動程式，會*使用 odbc 3.x 應用程式*或符合標準的應用程式，當它是使用 odbc 3.x 標頭檔進行編譯並*與 odbc 3.x* *程式庫相*連結時，以及當應用程式透過 odbc *3.x 驅動程式*管理員取得驅動程式的存取權時。  
  
 符合標準的應用程式和驅動程式會使用 ODBC_STD 編譯旗標進行編譯。  
  
 符合標準的應用程式會展示下列行為：  
  
-   如果符合標準的應用程式會呼叫**SQLAllocEnv** （這可能是因為**SQLAllocEnv**是 OPEN Group 和 ISO CLI 中的有效函式），則呼叫會在編譯時期對應至**SQLAllocHandleStd** 。 因此，在執行時間，應用程式會呼叫**SQLAllocHandleStd**。 在處理此呼叫的過程中，驅動程式管理員會將 SQL_ATTR_ODBC_VERSION 環境屬性設定為 SQL_OV_ODBC3。 呼叫**SQLAllocHandleStd**相當於呼叫具有*HandleType* SQL_HANDLE_ENV 的**SQLAllocHandle** ，以及呼叫**SQLSetEnvAttr**來設定 SQL_OV_ODBC3 SQL_ATTR_ODBC_VERSION。  
  
-   如果符合標準的應用程式呼叫**SQLBindParam** （可能是因為**SQLBindParam**是 OPEN Group 和 ISO CLI 中的有效函式），*則 ODBC 3.x*驅動程式管理員會將呼叫對應至**SQLBindParameter**中的對等呼叫。 （如需回溯相容性，請參閱附錄 G：驅動程式方針中的[SQLBindParam 對應](../../../odbc/reference/appendixes/sqlbindparam-mapping.md)）。  
  
-   為了配合 ISO CLI *，ODBC 3.x*標頭檔包含呼叫**SQLGetInfo**時所使用之資訊類型的別名。 符合標準的應用程式可以使用這些別名，而不是*ODBC 3.x 資訊類型。* 如需詳細資訊，請參閱下一個主題 [[標頭檔](../../../odbc/reference/develop-app/header-files.md)]。  
  
-   符合標準的應用程式必須確認其支援的所有功能都可在其所使用的驅動程式中受到支援。 將 SQL_ATTR_CURSOR_SCROLLABLE 語句屬性設定為 SQL_SCROLLABLE，並將 SQL_ATTR_CURSOR_SENSITIVITY 語句屬性設定為 SQL_INSENSITIVE 或 SQL_SENSITIVE 是標準中可用的選擇性功能，但不包含在 ODBC 3.x 核心層級中的功能，因此可能不會受到*所有 odbc 3.x* *驅動程式*的支援。 如果符合標準的應用程式使用這些功能，則應確認其所使用的驅動程式可支援它們。
