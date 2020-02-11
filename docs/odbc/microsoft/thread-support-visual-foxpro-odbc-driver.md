---
title: 執行緒支援（Visual FoxPro ODBC Driver） |Microsoft Docs
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
ms.openlocfilehash: 72672cfc20b5d363229fd1ba49278d11e6d6793d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67912409"
---
# <a name="thread-support-visual-foxpro-odbc-driver"></a>執行緒支援 (Visual FoxPro ODBC Driver)
Visual FoxPro ODBC 驅動程式是安全線程。 環境控制碼（*當*）、連接控制碼（*hdbc*）和語句控制碼（*hstmt*）的存取會包裝在適當的信號中，以防止其他進程存取，而且可能會改變驅動程式的內部資料結構。  
  
 在多執行緒應用程式中，您可以在個別的執行緒上呼叫[SQLCancel](../../odbc/microsoft/sqlcancel-visual-foxpro-odbc-driver.md) ，以取消在*hstmt*上同步執行的函式。  
  
 當您使用漸進式提取時，驅動程式會使用個別的執行緒來提取資料。 若要針對資料來源使用漸進式提取，請在 [ [ODBC Visual FoxPro 安裝程式] 對話方塊](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)上選取 [**在背景中提取資料**] 核取方塊，或在連接字串中使用 BackgroundFetch 屬性關鍵字。 當您從多執行緒應用程式呼叫驅動程式時，請避免使用背景提取。 如需連接字串屬性關鍵字的詳細資訊，請參閱[使用連接字串](../../odbc/microsoft/using-connection-strings.md)。  
  
 如需執行緒和**SQLCancel**的詳細資訊，請參閱 ODBC 程式設計*人員參考*中的[SQLCancel](../../odbc/reference/syntax/sqlcancel-function.md) 。
