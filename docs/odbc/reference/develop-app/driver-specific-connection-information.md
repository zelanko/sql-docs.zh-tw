---
title: 特定於驅動程式的連接資訊 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 16c8c5fc4fd3ac63aa3613b41e530446dffec118
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305787"
---
# <a name="driver-specific-connection-information"></a>特定驅動程式的連線資訊
**SQLConnect**假定數據來源名稱、使用者 ID 和密碼足以連接到數據源,並且所有其他連接資訊可以存儲在系統上。 情況通常並非如此。 例如,驅動程式可能需要一個使用者 ID 和密碼才能登錄到伺服器,需要不同的使用者 ID 和密碼才能登錄到 DBMS。 由於**SQLConnect**接受單個使用者 ID 和密碼,這意味著如果要使用**SQLConnect,** 則必須將其他使用者 ID 和密碼與系統上的資料源資訊一起儲存。 這是潛在的安全漏洞,除非密碼被加密,否則應避免這樣做。  
  
 **SQLDriverConnect**允許驅動程式在連接字串的關鍵字值對中定義任意數量的連接資訊。 例如,假設驅動程式需要數據源名稱、伺服器的使用者 ID 和密碼以及 DBMS 的使用者 ID 和密碼。 在 XYZ Corp 資料來源的自訂程式可能會提示使用者輸入 ID 和密碼,並建構以下一組關鍵字-值對或*連接字串,* 以傳遞給**SQLDriverConnect**:  
  
> [!NOTE]  
>  如果要連接到支援 Windows 身份驗證的資料來源提供者,則應在連接字串`Trusted_Connection=yes`中指定 而不是使用者 ID 和密碼資訊。  
  
```  
DSN={MyDataSourceName};UID={MyUserID};PWD={MyServerPassword};UIDDBMS={MyDBMSUserID};PWDDBMS={MyDBMSUserPassword};  
```  
  
 **DSN(** 資料來源名稱)關鍵字為資料源命名 **,UID**和**PWD**關鍵字指定伺服器的使用者 ID 和密碼 **,UIDDBMS**和**PWDDBMS**關鍵字指定 DBMS 的使用者 ID 和密碼。 請注意,最終分號是可選的。 **SQLDriverConnect**解析此字串;使用 XYZ Corp 資料來源名稱從系統檢索其他連接資訊,例如伺服器位址;並使用指定的用戶密碼登錄到伺服器和 DBMS。  
  
 **SQLDriverConnect**中的關鍵字值對必須遵循某些語法規則。 關鍵字及其值不應包含**{}*(""""""""""""""""""""""""""""""""""""""""\*[!]** 字元。 **DSN**關鍵字的值不能僅包含空白,並且不應包含前導空格。 由於註冊表語法,關鍵字和數據源名稱不能包含反斜杠\\( ) 字元。 關鍵字值對中的等號周圍不允許空格。  
  
 在呼叫**SQLDriverConnect**時,可以使用**FILESN**關鍵字指定包含資料來源資訊的檔的名稱(請參閱本節後面的[「使用檔案數據源進行連接](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md))。 **SAVEFILE**關鍵字可用於指定 .dsn 檔案的名稱,其中將保存調用**SQLDriverConnect**成功連接的關鍵字-值對。 有關文件數據源的詳細資訊,請參閱[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)函數說明。
