---
title: 以 DBMS 為基礎的驅動程式診斷範例 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DBMS-based driver diagnostic [ODBC]
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: a80d54b0-43ff-4dfd-b6cb-f4694a5ed765
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 117f43548d2b57233dea6f7423e6bad67b6233b0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304349"
---
# <a name="dbms-based-driver-diagnostic-example"></a>以 DBMS 為基礎的驅動程式診斷範例
以 DBMS 為基礎的驅動程式會將要求傳送至 DBMS，並透過驅動程式管理員將資訊傳回到應用程式。 因為驅動程式是與驅動程式管理員介面的元件，所以它會格式化並傳回**SQLGetDiagRec**的引數。  
  
 例如，如果使用 SQL/服務，則適用于 Oracle Rdb 的 Microsoft 驅動程式遇到不正確資料指標名稱，它可能會從**SQLGetDiagRec**傳回下列值：  
  
```  
SQLSTATE:         "34000"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Rdb Driver]Invalid cursor name: EMPLOYEE_CURSOR."  
```  
  
 因為此錯誤發生在驅動程式中，所以它會將前置詞新增至廠商的診斷訊息（[Microsoft]）和驅動程式（[ODBC Rdb 驅動程式]）。  
  
 如果 DBMS 找不到資料表 EMPLOYEE，驅動程式可能會格式化，並從**SQLGetDiagRec**傳回下列值：  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1  
Diagnostic Msg:   "[Microsoft][ODBC Rdb Driver][Rdb] %SQL-F-RELNOTDEF, Table EMPLOYEE "  
                  "is not defined in schema."  
```  
  
 因為此錯誤發生在資料來源中，所以驅動程式已在診斷訊息中加入資料來源識別碼（[Rdb]）的前置詞。 因為驅動程式是與資料來源介面的元件，所以它會將其廠商的前置詞（[Microsoft]）和識別碼（[ODBC Rdb 驅動程式]）新增至診斷訊息。
