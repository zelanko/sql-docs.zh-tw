---
title: 使用作業系統身份驗證 :微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], authentication
- authentication [ODBC]
ms.assetid: 613daef7-3171-42d0-b7e3-3879280f864d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d6520202bdbc31baf1156531457cb70a98656e88
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292838"
---
# <a name="using-operating-system-authentication"></a>使用作業系統驗證
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 而是使用 Oracle 提供的 ODBC 驅動程式。  
  
 Oracle 作業系統身份驗證依賴於基礎操作系統來控制對資料庫帳戶的訪問。 使用此類登錄時,使用者無需輸入密碼。  
  
 要利用此功能,請將「/」指定為使用者 ID,並且在使用以下任何連接 API 連線時不要指定密碼[:SQLBrowseConnect、SQLConnect](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md)或[SQLConnect](../../odbc/microsoft/core-level-api-functions-odbc-driver-for-oracle.md)[SQLDriverConnect](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md)。  
  
 Oracle 資料庫使用 SQL_Net 驗證服務對登入的使用者進行身份驗證。 如果用戶通過 SQLPlus 登錄到 Oracle,則此服務效果良好;但是,當登錄使用者是 Internet 資訊服務等服務時,身份驗證將失敗。 這是 SQL\*Net 身份驗證的已知限制,並產生以下錯誤:"[Oracle[Oracle]ORA_12641:TNS:身份驗證服務無法初始化。  
  
 您可以通過編輯 Sqlnet.ora 檔案來更正此問題。 此設定檔通常儲存在 Oracle 家目錄的 Network_Admin 子目錄中。 將以下行新增到 Sqlnet.ora:  
  
```  
SQLNET.AUTHENTICATION_SERVICES = (none)  
```
