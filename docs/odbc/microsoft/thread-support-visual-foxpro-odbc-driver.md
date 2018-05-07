---
title: 執行緒支援 （Visual FoxPro ODBC 驅動程式） |Microsoft 文件
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
- thread support [ODBC]
- Visual FoxPro ODBC driver [ODBC], thread support
- FoxPro ODBC driver [ODBC], thread support
- multithreaded applications [ODBC]
ms.assetid: 0c6abbbc-012b-41aa-bded-5e7e362d015b
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 75adc2f72071765dc705d34b2bdd577316ae1acf
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="thread-support-visual-foxpro-odbc-driver"></a>執行緒支援 （Visual FoxPro ODBC 驅動程式）
Visual FoxPro ODBC 驅動程式是安全執行緒。 存取權的環境控制代碼 (*匣*)，連接控制代碼 (*hdbc*)，和陳述式控制代碼 (*hstmt*) 會包裝在適當的號誌，以防止其他處理程序從存取，可能會改變驅動程式的內部資料結構。  
  
 在多執行緒應用程式中，您可以取消同步執行的函式*hstmt*藉由呼叫[SQLCancel](../../odbc/microsoft/sqlcancel-visual-foxpro-odbc-driver.md)另一個執行緒上。  
  
 驅動程式會使用個別執行緒，當您使用漸進式提取時擷取資料。 若要使用漸進式擷取的資料來源，請選取**提取資料，在背景中的** 核取方塊[ODBC Visual FoxPro 安裝程式對話方塊](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)或 BackgroundFetch 屬性關鍵字用於您的連線字串。 避免多執行緒應用程式呼叫驅動程式時，使用背景擷取。 連接字串屬性關鍵字的詳細資訊，請參閱[使用連接字串](../../odbc/microsoft/using-connection-strings.md)。  
  
 如需執行緒的詳細資訊和**SQLCancel**，請參閱[SQLCancel](../../odbc/reference/syntax/sqlcancel-function.md)中*ODBC 程式設計人員參考*。
