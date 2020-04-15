---
title: Unicode 資料 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC], data
- data types [ODBC], Unicode
- C data types [ODBC], Unicode
- SQL data types [ODBC], Unicode
ms.assetid: abc28718-e6d9-49fb-97ff-402d50c3c375
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 73ea9035b05f04fec1527ca2aa98531a807db8cf
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307395"
---
# <a name="unicode-data"></a>Unicode 資料
提供 SQL Unicode 數據類型來描述駐留在 DBMS 上的 Unicode 本機數據。 提供了 C Unicode 資料類型,允許應用程式將數據綁定到 Unicode 緩衝區。 驅動程式管理員可以從 Unicode C 類型 (SQL_C_WCHAR) 轉換數據,使其與 ANSI 驅動程式一起執行。  
  
 ODBC 3.0 或 2。*x*應用程式將始終綁定到 ANSI 資料類型。 為獲得最佳性能,如果 SQL 列類型為 ANSI,則 ODBC 3.5(或更高)應用程式應綁定到 ANSI 資料類型,如果 SQL 列類型為 Unicode,則應綁定到 Unicode C 數據類型。  
  
 SQL Unicode 類型指示器SQL_WCHAR、SQL_WVARCHAR和SQL_WLONGVARCHAR。 SQL_WCHAR資料具有固定的字串長度,而SQL_WVARCHAR具有具有聲明最大值的可變長度,並且SQL_WLONGVARCHAR具有變數長度,最大值取決於數據源。  
  
 C Unicode 類型指示器SQL_C_WCHAR。 這是每個 SQL Unicode 類型指標的預設值。 所有 SQL 類型都可以轉換為SQL_C_WCHAR,並且SQL_C_WCHAR可以轉換為所有 SQL 類型。 應用程式可以通過三種方式之一檢索數據:  
  
-   以SQL_C_CHAR身份檢索數據。  
  
-   以SQL_C_WCHAR檢索數據。  
  
-   將數據聲明為SQL_C_TCHAR。 這是一個宏,用於插入SQL_C_WCHAR如果應用程式編譯為 Unicode 應用程式,或者SQL_C_CHAR(如果應用程式編譯為 ANSI 應用程式)插入。  
  
 SQL_C_TCHAR在函數中聲明,如下所示:  
  
```  
SQLBindParameter(StatementHandle, 1, SQL_PARAM_INPUT, SQL_C_TCHAR, SQL_WCHAR, NameLen, 0, Name, 0, &Name)  
```  
  
 當應用程式編譯為 Unicode 應用程式時 *,ValueType*參數將從SQL_C_TCHAR更改為SQL_C_WCHAR。 當應用程式編譯為 ANSI 應用程式時 *,ValueType*參數將更改為SQL_C_CHAR。  
  
 Unicode 驅動程式仍必須支援 ANSI 資料類型,包括SQL_CHAR。 如果使用 Unicode 驅動程式的應用程式綁定到SQL_CHAR,驅動程式管理器將不會將SQL_CHAR數據映射到SQL_WCHAR。 Unicode 驅動程式必須接受SQL_CHAR數據。  
  
 驅動程式管理員在 Unicode 中儲存驅動程式和 DSN 名稱,並根據需要將其映射到 ANSI。 如果 Unicode 字元無法映射到 ANSI 字元(如果驅動程式和 DSN 名稱中使用了非電腦本機代碼頁的代碼頁的字元,則無法轉換的字元由系統提供的預設字元表示。
