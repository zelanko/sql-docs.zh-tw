---
description: Unicode 資料
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f217e6b629936cc835d134c89d972bb1408b9d0b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88339114"
---
# <a name="unicode-data"></a>Unicode 資料
系統會提供 SQL Unicode 資料類型，以原生方式描述 DBMS 上的 Unicode 資料。 系統會提供 C Unicode 資料類型，以允許應用程式將資料系結至 Unicode 緩衝區。 驅動程式管理員可以將 Unicode C 類型的資料轉換 (SQL_C_WCHAR) ，讓它能夠搭配 ANSI 驅動程式運作。  
  
 ODBC 3.0 或2。*x* 應用程式一律會系結至 ANSI 資料類型。 為了達到最佳效能，如果 sql 資料行類型是 ANSI，ODBC 3.5 (或更高的) 應用程式應該系結至 ANSI 資料 C 類型，如果 SQL 資料行類型是 Unicode，則應該系結至 Unicode C 資料類型。  
  
 SQL Unicode 類型指標是 SQL_WCHAR、SQL_WVARCHAR 和 SQL_WLONGVARCHAR。 SQL_WCHAR 資料具有固定的字串長度，而 SQL_WVARCHAR 的變數長度為已宣告的最大值，且 SQL_WLONGVARCHAR 具有最大值（取決於資料來源）的可變長度。  
  
 C Unicode 類型指標是 SQL_C_WCHAR。 這是每個 SQL Unicode 類型指標的預設值。 所有 SQL 類型都可以轉換成 SQL_C_WCHAR，而且 SQL_C_WCHAR 可以轉換成所有的 SQL 類型。 應用程式可以使用下列三種方式之一來取得資料：  
  
-   SQL_C_CHAR 取得資料。  
  
-   SQL_C_WCHAR 取得資料。  
  
-   將資料宣告為 SQL_C_TCHAR。 如果應用程式編譯為 Unicode 應用程式，或是在編譯為 ANSI 應用程式的情況下插入 SQL_C_CHAR，則這是插入 SQL_C_WCHAR 的宏。  
  
 在函式中宣告 SQL_C_TCHAR，如下所示：  
  
```  
SQLBindParameter(StatementHandle, 1, SQL_PARAM_INPUT, SQL_C_TCHAR, SQL_WCHAR, NameLen, 0, Name, 0, &Name)  
```  
  
 當應用程式編譯為 Unicode 應用程式時，會將 *ValueType* 引數從 SQL_C_TCHAR 變更為 SQL_C_WCHAR。 當應用程式編譯為 ANSI 應用程式時，會將 *ValueType* 引數變更為 SQL_C_CHAR。  
  
 Unicode 驅動程式仍然必須支援 ANSI 資料類型，包括 SQL_CHAR。 如果使用 Unicode 驅動程式的應用程式系結至 SQL_CHAR，驅動程式管理員將不會將 SQL_CHAR 的資料對應至 SQL_WCHAR。 Unicode 驅動程式必須接受 SQL_CHAR 的資料。  
  
 驅動程式管理員會以 Unicode 儲存驅動程式和 DSN 名稱，並視需要將它們對應至 ANSI。 如果 Unicode 字元無法對應至 ANSI 字元 (如有可能發生在驅動程式和 DSN) 名稱所使用的字碼頁中的字元不是電腦的機器碼，則無法轉換的字元會以系統提供的預設字元表示。
