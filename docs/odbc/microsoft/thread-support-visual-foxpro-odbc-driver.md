---
title: 執行緒支援 (Visual FoxPro ODBC Driver) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- thread support [ODBC]
- Visual FoxPro ODBC driver [ODBC], thread support
- FoxPro ODBC driver [ODBC], thread support
- multithreaded applications [ODBC]
ms.assetid: 0c6abbbc-012b-41aa-bded-5e7e362d015b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 77187802bb57a832263ec2070564754e87f21345
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62632921"
---
# <a name="thread-support-visual-foxpro-odbc-driver"></a>執行緒支援 (Visual FoxPro ODBC Driver)
Visual FoxPro ODBC Driver 是安全執行緒。 存取權的環境控制代碼 (*h*)，連接控制代碼 (*hdbc*)，以及陳述式控制代碼 (*hstmt*) 包裝在適當的號誌，以防止其他處理序從存取，而可能變更驅動程式的內部資料結構。  
  
 在多執行緒應用程式中，您可以取消同步執行的函式*hstmt*藉由呼叫[SQLCancel](../../odbc/microsoft/sqlcancel-visual-foxpro-odbc-driver.md)另一個執行緒上。  
  
 驅動程式會使用個別的執行緒，當您使用漸進式提取時擷取資料。 若要使用漸進式擷取的資料來源，請選取**提取中背景的資料** 核取方塊[ODBC Visual FoxPro 設定對話方塊](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)或 BackgroundFetch 屬性關鍵字用於您的連線字串。 請避免使用背景擷取，當您從多執行緒應用程式中呼叫 驅動程式。 如需連接字串屬性關鍵字的詳細資訊，請參閱[使用的連接字串](../../odbc/microsoft/using-connection-strings.md)。  
  
 如需執行緒的詳細資訊和**SQLCancel**，請參閱[SQLCancel](../../odbc/reference/syntax/sqlcancel-function.md)中*ODBC 程式設計人員參考*。
