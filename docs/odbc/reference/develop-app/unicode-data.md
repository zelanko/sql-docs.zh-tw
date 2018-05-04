---
title: Unicode 資料 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC], data
- data types [ODBC], Unicode
- C data types [ODBC], Unicode
- SQL data types [ODBC], Unicode
ms.assetid: abc28718-e6d9-49fb-97ff-402d50c3c375
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7871576f95ebb49708036d531c4f2d8eebbac863
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="unicode-data"></a>Unicode 資料
提供 SQL Unicode 資料類型來描述存在於以 Unicode 原生上 DBMS 的資料。 C Unicode 資料類型可讓應用程式將資料繫結至 Unicode 的緩衝區。 驅動程式管理員可以將資料轉換的 Unicode C 類型 (SQL_C_WCHAR)，使其從 ANSI 驅動程式的函式。  
  
 ODBC 3.0 或 2。*x*應用程式一律會繫結至 ANSI 資料類型。 為了取得最佳效能，ODBC 3.5 （或更新版本） 應用程式應為 ANSI C 資料類型繫結，如果 SQL 資料行類型為 ANSI，而且應該繫結到 Unicode C 資料類型的 SQL 資料行型別是否為 Unicode。  
  
 SQL Unicode 類型指標為 SQL_WCHAR、 SQL_WVARCHAR 和 SQL_WLONGVARCHAR。 SQL_WCHAR 資料具有固定的字串長度，而 SQL_WVARCHAR 長度變數宣告最多可 SQL_WLONGVARCHAR 具有可變長度的資料來源而定，最多。  
  
 C Unicode 類型指標為 SQL_C_WCHAR。 這是每個 SQL Unicode 類型指標的預設值。 所有的 SQL 型別可以轉換為 SQL_C_WCHAR 等 SQL_C_WCHAR 可以轉換為所有的 SQL 類型。 應用程式可以擷取資料中有三種：  
  
-   SQL_C_CHAR 的形式擷取資料。  
  
-   做為 SQL_C_WCHAR 擷取資料。  
  
-   宣告 SQL_C_TCHAR 資料。 這是插入 SQL_C_WCHAR，如果應用程式會編譯為在 Unicode 應用程式，或插入 SQL_C_CHAR 就會編譯為 ANSI 應用程式的巨集。  
  
 SQL_C_TCHAR 被宣告的函式，如下所示：  
  
```  
SQLBindParameter(StatementHandle, 1, SQL_PARAM_INPUT, SQL_C_TCHAR, SQL_WCHAR, NameLen, 0, Name, 0, &Name)  
```  
  
 當應用程式會編譯為在 Unicode 應用程式， *ValueType*引數會從 SQL_C_TCHAR 變成 SQL_C_WCHAR。 當應用程式會編譯為 ANSI 應用程式， *ValueType*引數會變更為 SQL_C_CHAR。  
  
 Unicode 驅動程式必須仍然支援 ANSI 資料類型，包括 SQL_CHAR。 如果使用 Unicode 驅動程式的應用程式繫結至 SQL_CHAR，驅動程式管理員將不會對應至 SQL_WCHAR SQL_CHAR 資料。 Unicode 驅動程式必須接受 SQL_CHAR 資料。  
  
 驅動程式管理員以 Unicode 來儲存驅動程式和資料來源名稱的名稱，並視需要將它們對應為 ANSI。 Unicode 字元無法對應至一個 ANSI 字元 （如如果驅動程式和 DSN 名稱中使用的字元不是電腦的原生程式碼頁的字碼頁，可能會發生），如果無法轉換的字元會以預設字元 supplied 系統。
