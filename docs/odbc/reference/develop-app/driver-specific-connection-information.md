---
title: 驅動程式特有的連接資訊 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLConnect function [ODBC], driver-specific connection information
- connecting to driver [ODBC], SQLConnect
- SQLDriverConnect function [ODBC], driver specific connection information
- connecting to data source [ODBC], SQLDriverConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], SQLConnect
- connecting to driver [ODBC], driver-specific information
ms.assetid: 3748758a-f16a-4f3b-9c40-06f2e300704e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e3852e713e517828e83e74bf7fb291ef20865532
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63238707"
---
# <a name="driver-specific-connection-information"></a>特定驅動程式的連線資訊
**SQLConnect**假設資料來源名稱、 使用者識別碼和密碼是足以連接至資料來源，而所有其他連接資訊，可以儲存在系統上。 這通常不是大小寫。 例如，驅動程式可能需要一位使用者識別碼和密碼登入伺服器以及不同的使用者識別碼和密碼來登入 DBMS。 因為**SQLConnect**接受單一使用者識別碼和密碼，這表示，其他使用者識別碼和密碼必須儲存在系統上的資料來源資訊如果**SQLConnect**用。 這是潛在安全性缺口，而且應該避免使用，除非密碼加密。  
  
 **SQLDriverConnect**讓驅動程式在連接字串的關鍵字-值組中定義任意數量的連接資訊。 例如，假設驅動程式需要的資料來源名稱、 使用者識別碼和密碼的伺服器，以及使用者識別碼和密碼用於 DBMS。 一律使用 XYZ Corp 資料來源的自訂程式可能會提示使用者輸入識別碼與密碼，並建置下列關鍵字-值配對，一組或*連接字串*要傳遞至**SQLDriverConnect**:  
  
> [!NOTE]  
>  如果您要連接到資料來源提供者支援 Windows 驗證，您應該指定`Trusted_Connection=yes`而不是在連接字串中的使用者識別碼和密碼資訊。  
  
```  
DSN={MyDataSourceName};UID={MyUserID};PWD={MyServerPassword};UIDDBMS={MyDBMSUserID};PWDDBMS={MyDBMSUserPassword};  
```  
  
 **DSN** （資料來源名稱） 關鍵字名稱資料來源， **UID**並**PWD**關鍵字指定的使用者識別碼和密碼的伺服器，而**UIDDBMS**並**PWDDBMS**關鍵字指定的使用者識別碼和密碼用於 DBMS。 請注意，最終的分號是選擇性的。 **SQLDriverConnect**剖析這個字串; 使用 XYZ Corp 資料來源名稱來擷取系統，例如伺服器位址; 中的其他連接資訊和登入伺服器和 DBMS，使用指定的使用者識別碼與密碼。  
  
 中的關鍵字-值配對**SQLDriverConnect**必須遵循特定語法規則。 這些關鍵字，而且其值不應包含 **[]{}(）; 嗎？\*= ！ @** 字元。 值**DSN**關鍵字不能只包含空格，且不能包含開頭空白。 因為登錄文法中，關鍵字和資料來源名稱不能包含反斜線 (\\) 字元。 中的關鍵字 / 值組的等號前後不能有空格。  
  
 **FILEDSN**呼叫中，可以使用關鍵字**SQLDriverConnect**來指定包含資料來源資訊的檔案名稱 (請參閱[連線使用檔案資料來源](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)稍後這一節)。 **SAVEFILE**關鍵字可用來指定的連線成功的關鍵字-值配對所做的.dsn 檔案名稱中的呼叫所**SQLDriverConnect**會儲存。 如需檔案資料來源的詳細資訊，請參閱[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)函式描述。
