---
title: "驅動程式特有的連接資訊 |Microsoft 文件"
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
- SQLConnect function [ODBC], driver-specific connection information
- connecting to driver [ODBC], SQLConnect
- SQLDriverConnect function [ODBC], driver specific connection information
- connecting to data source [ODBC], SQLDriverConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], SQLConnect
- connecting to driver [ODBC], driver-specific information
ms.assetid: 3748758a-f16a-4f3b-9c40-06f2e300704e
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e027eb6b5c5afdf361854892a22ad5dd69a9d646
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="driver-specific-connection-information"></a>驅動程式特有的連接資訊
**SQLConnect**假設資料來源名稱、 使用者識別碼和密碼是足以連接至資料來源，而所有其他連接資訊，可以儲存在系統上。 這通常不是大小寫。 例如，驅動程式可能需要一位使用者 ID 和密碼登入伺服器以及不同的使用者識別碼和密碼來登入 DBMS。 因為**SQLConnect**接受單一使用者識別碼和密碼，這表示，其他使用者識別碼和密碼必須儲存在系統上的資料來源資訊如果**SQLConnect**使用。 這是潛在的安全性漏洞，而且應該避免使用，除非密碼加密。  
  
 **SQLDriverConnect**讓驅動程式在連接字串關鍵字-值配對中定義任意數量的連接資訊。 例如，假設驅動程式需要的資料來源名稱、 使用者識別碼和密碼的伺服器，以及使用者識別碼和密碼的 DBMS。 一律使用 XYZ Corp 資料來源的自訂程式可能會提示使用者輸入 Id 和密碼，並建立下列關鍵字-值組集合，或*連接字串*要傳遞給**SQLDriverConnect**:  
  
> [!NOTE]  
>  如果您要連接至資料來源提供者支援 Windows 驗證，您應該指定`Trusted_Connection=yes`而不是在連接字串中的使用者識別碼和密碼資訊。  
  
```  
DSN={MyDataSourceName};UID={MyUserID};PWD={MyServerPassword};UIDDBMS={MyDBMSUserID};PWDDBMS={MyDBMSUserPassword};  
```  
  
 **DSN** （資料來源名稱） 關鍵字名稱資料來源， **UID**和**PWD**關鍵字指定的使用者識別碼和密碼的伺服器，而**UIDDBMS**和**PWDDBMS**關鍵字指定的使用者識別碼和密碼的 DBMS。 請注意，最後以分號是選擇性的。 **SQLDriverConnect**剖析這個字串，則使用 XYZ Corp 資料來源名稱從系統中，例如伺服器位址; 擷取的其他連接資訊和登入伺服器並使用指定的使用者識別碼和密碼的 DBMS。  
  
 中的關鍵字-值配對**SQLDriverConnect**必須遵循特定的語法規則。 這些關鍵字，而且其值不應該包含**[] {} （)，;？\*= ！ @**字元。 值**DSN**關鍵字不能只包含空格，且不能包含前置的空白。 因為登錄文法中，關鍵字和資料來源名稱不能包含反斜線 (\\) 字元。 關鍵字-值配對中的等號前後不能有空格。  
  
 **FILEDSN**關鍵字可用於呼叫**SQLDriverConnect**來指定包含資料來源資訊的檔案名稱 (請參閱[連接使用的檔案資料來源](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)，本主題稍後)。 **SAVEFILE**關鍵字可用來指定的連線成功的關鍵字-值配對所做的.dsn 檔案名稱中的呼叫所**SQLDriverConnect**將會儲存。 如需檔案資料來源的詳細資訊，請參閱[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)函式描述。
