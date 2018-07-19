---
title: 使用作業系統驗證 |Microsoft 文件
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
- ODBC driver for Oracle [ODBC], authentication
- authentication [ODBC]
ms.assetid: 613daef7-3171-42d0-b7e3-3879280f864d
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 335e8aca1a54b2f70a34d9e504985c12d08597bc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32905756"
---
# <a name="using-operating-system-authentication"></a>使用作業系統驗證
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，使用由 Oracle 提供的 ODBC 驅動程式。  
  
 Oracle 系統驗證會依賴基礎作業系統來控制資料庫帳戶的存取權。 當使用這種類型的登入，使用者不需要輸入密碼。  
  
 若要使用這項功能，請指定"/"作為使用者識別碼並不會指定密碼時使用下列連線應用程式開發介面的任何連線： [SQLBrowseConnect](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md)， [SQLConnect](../../odbc/microsoft/core-level-api-functions-odbc-driver-for-oracle.md)，或[SQLDriverConnect](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md)。  
  
 Oracle 資料庫使用 SQL * Net 驗證服務來驗證登入的使用者。 使用者登入 Oracle 透過 SQLPlus; 如果此服務的運作方式不過，例如網際網路資訊服務的服務登入使用者時，驗證將會失敗。 這是 SQL 的已知的限制\*網路驗證，並產生下列錯誤: 「 [Microsoft] [oracle 的 ODBC 驅動程式] [Oracle] 或 12641: TNS:authentication 服務無法初始化。 」  
  
 您可以藉由編輯 Sqlnet.ora 檔案來修正此問題。 此組態檔通常會儲存 Oracle 主目錄的 Network\Admin 子目錄中。 將下列行加入至 Sqlnet.ora:  
  
```  
SQLNET.AUTHENTICATION_SERVICES = (none)  
```
