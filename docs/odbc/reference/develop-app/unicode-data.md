---
title: Unicode 資料 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 899924b5c0847d5f42e383a9e04c33298bb368b9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68087750"
---
# <a name="unicode-data"></a>Unicode 資料
系統會提供 SQL Unicode 資料類型，以原生方式描述 DBMS 上以 Unicode 表示的資料。 提供 C Unicode 資料類型，以允許應用程式將資料系結至 Unicode 緩衝區。 驅動程式管理員可以轉換 Unicode C 類型的資料（SQL_C_WCHAR），使其與 ANSI 驅動程式搭配運作。  
  
 ODBC 3.0 或2。*x*應用程式一律會系結至 ANSI 資料類型。 為了達到最佳效能，如果 sql 資料行類型是 ANSI，ODBC 3.5 （或更新版本）應用程式應該系結至 ANSI 資料 C 類型，如果 SQL 資料行類型為 Unicode，則應系結至 Unicode C 資料類型。  
  
 SQL Unicode 類型指標是 SQL_WCHAR、SQL_WVARCHAR 和 SQL_WLONGVARCHAR。 SQL_WCHAR 資料具有固定的字串長度，而 SQL_WVARCHAR 的可變長度具有已宣告的最大值，而且 SQL_WLONGVARCHAR 具有與資料來源相依之最大值的可變長度。  
  
 C Unicode 類型指標是 SQL_C_WCHAR。 這是每個 SQL Unicode 型別指標的預設值。 所有 SQL 類型都可以轉換成 SQL_C_WCHAR，而且 SQL_C_WCHAR 可以轉換成所有 SQL 類型。 應用程式可以使用下列三種方式之一來捕獲資料：  
  
-   取得 SQL_C_CHAR 的資料。  
  
-   取得 SQL_C_WCHAR 的資料。  
  
-   將資料宣告為 SQL_C_TCHAR。 這個宏會在應用程式編譯為 Unicode 應用程式時插入 SQL_C_WCHAR，如果編譯為 ANSI 應用程式，則插入 SQL_C_CHAR。  
  
 在函式中宣告 SQL_C_TCHAR，如下所示：  
  
```  
SQLBindParameter(StatementHandle, 1, SQL_PARAM_INPUT, SQL_C_TCHAR, SQL_WCHAR, NameLen, 0, Name, 0, &Name)  
```  
  
 當應用程式編譯為 Unicode 應用程式時， *ValueType*引數會從 SQL_C_TCHAR 變更為 SQL_C_WCHAR。 當應用程式編譯為 ANSI 應用程式時， *ValueType*引數會變更為 SQL_C_CHAR。  
  
 Unicode 驅動程式仍然必須支援 ANSI 資料類型，包括 SQL_CHAR。 如果應用程式使用 Unicode 驅動程式系結至 SQL_CHAR，驅動程式管理員將不會將 SQL_CHAR 資料對應至 SQL_WCHAR。 Unicode 驅動程式必須接受 SQL_CHAR 的資料。  
  
 驅動程式管理員會以 Unicode 儲存驅動程式和 DSN 名稱，並視需要將它們對應至 ANSI。 如果 Unicode 字元不能對應至 ANSI 字元（在驅動程式和 DSN 名稱中使用不是電腦的機器碼頁之字碼頁中的字元，就會發生這種情況），無法轉換的字元會以預設字元 sup 表示由系統 plied。
