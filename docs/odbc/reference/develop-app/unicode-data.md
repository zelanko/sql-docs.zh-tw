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
manager: craigg
ms.openlocfilehash: 74de6c44aaf109a434f0cf76c6902abfba92efe1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63305764"
---
# <a name="unicode-data"></a>Unicode 資料
SQL Unicode 資料類型可供描述位於 Unicode 原生方式在 DBMS 的資料。 C Unicode 資料類型可讓應用程式將資料繫結至 Unicode 的緩衝區。 驅動程式管理員可以將資料轉換從 Unicode C 類型 (SQL_C_WCHAR)，以便與 ANSI 驅動程式的函式。  
  
 ODBC 3.0 或 2。*x*應用程式一律會繫結至的 ANSI 資料類型。 為了取得最佳效能，ODBC 3.5 （或更新版本） 應用程式應該以 ANSI C 資料類型繫結，如果 SQL 資料行類型為 ANSI，而且應該繫結到 Unicode C 資料類型的 SQL 資料行型別是否為 Unicode。  
  
 SQL Unicode 類型指標是 SQL_WCHAR、 SQL_WVARCHAR 和 SQL_WLONGVARCHAR。 SQL_WCHAR 資料具有固定的字串長度，SQL_WVARCHAR 具有可變長度的宣告的最大值而 SQL_WLONGVARCHAR 具有可變長度取決於資料來源的最大。  
  
 C Unicode 類型指標為 SQL_C_WCHAR。 這是每個 SQL Unicode 類型指標的預設值。 所有的 SQL 類型可轉換成 SQL_C_WCHAR 等 SQL_C_WCHAR 可以轉換為所有的 SQL 類型。 應用程式可以擷取資料中有三種：  
  
-   為 SQL_C_CHAR 擷取資料。  
  
-   擷取資料做為 SQL_C_WCHAR。  
  
-   資料可以宣告為 SQL_C_TCHAR。 這是插入 SQL_C_WCHAR，如果應用程式編譯成 Unicode 應用程式，或如果它編譯為 ANSI 應用程式，插入 SQL_C_CHAR 巨集。  
  
 SQL_C_TCHAR 中宣告的函式，如下所示：  
  
```  
SQLBindParameter(StatementHandle, 1, SQL_PARAM_INPUT, SQL_C_TCHAR, SQL_WCHAR, NameLen, 0, Name, 0, &Name)  
```  
  
 應用程式編譯為 Unicode 應用程式時*ValueType*引數會從 SQL_C_TCHAR 變成 SQL_C_WCHAR。 應用程式編譯為 ANSI 應用程式時*ValueType*引數會變更為 SQL_C_CHAR。  
  
 Unicode 驅動程式仍然必須支援 ANSI 資料類型，包括 SQL_CHAR。 如果使用 Unicode 驅動程式的應用程式繫結至 SQL_CHAR，驅動程式管理員將不會對應至 SQL_WCHAR SQL_CHAR 資料。 Unicode 驅動程式必須接受 SQL_CHAR 資料。  
  
 驅動程式管理員以 Unicode 來儲存驅動程式和 DSN 名稱，並視需要將它們對應成 ANSI。 Unicode 字元無法對應至一個 ANSI 字元 （因為如果不是電腦的原生程式碼頁的字碼頁的字元和使用的驅動程式 DSN 名稱，可能會發生），如果無法轉換的字元會以預設字元 supplied 系統。
