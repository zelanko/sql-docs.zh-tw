---
title: 使用作業系統驗證 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5a532c253ea2204fa3636c24c503cbefd3fa6311
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63127817"
---
# <a name="using-operating-system-authentication"></a>使用作業系統驗證
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，使用所提供的 ODBC 驅動程式。  
  
 Oracle 作業系統驗證依賴基礎作業系統來控制資料庫帳戶的存取權。 當使用這種類型的登入，使用者不需要輸入密碼。  
  
 若要利用這項功能，請指定"/"作為使用者識別碼和使用任何下列的 Api 連線進行連線時未指定密碼：[SQLBrowseConnect](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md)， [SQLConnect](../../odbc/microsoft/core-level-api-functions-odbc-driver-for-oracle.md)，或[SQLDriverConnect](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md)。  
  
 Oracle 資料庫使用 SQL * Net 的驗證服務，來驗證登入的使用者。 這項服務適用於使用者登入 SQLPlus; 透過 Oracle不過，例如 Internet Information Services 的服務登入的使用者時，驗證將會失敗。 這是已知的限制，SQL 的\*Net 的驗證，並產生下列錯誤: 「 [Microsoft] [ODBC driver for Oracle] [Oracle] ORA-12641:TNS:authentication 服務無法初始化。 」  
  
 您可以藉由編輯 Sqlnet.ora 檔案來修正此問題。 此組態檔通常會儲存在 Oracle 主目錄的 Network\Admin 子目錄中。 將下行新增至 Sqlnet.ora 中：  
  
```  
SQLNET.AUTHENTICATION_SERVICES = (none)  
```
