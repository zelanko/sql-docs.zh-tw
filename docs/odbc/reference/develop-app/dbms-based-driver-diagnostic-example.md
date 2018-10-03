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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0485ecf720cb84580c17c77b31fc6816de2e679a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47622266"
---
# <a name="dbms-based-driver-diagnostic-example"></a>以 DBMS 為基礎的驅動程式診斷範例
以 DBMS 為基礎的驅動程式將要求傳送至 DBMS，並傳回至應用程式透過驅動程式管理員的資訊。 因為驅動程式介面驅動程式管理員使用的元件，其格式，並傳回引數**SQLGetDiagRec**。  
  
 比方說，如果針對 Oracle Rdb 遇到無效的資料指標名稱，請使用 SQL/服務，Microsoft 驅動程式，它可能會傳回下列值從**SQLGetDiagRec**:  
  
```  
SQLSTATE:         "34000"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Rdb Driver]Invalid cursor name: EMPLOYEE_CURSOR."  
```  
  
 驅動程式中發生的錯誤，所以它加入前置詞的診斷訊息 ([Microsoft]) 的廠商和驅動程式 （[ODBC Rdb 驅動程式]）。  
  
 如果 DBMS 找不到員工的資料表，驅動程式可能會格式化，並傳回下列值從**SQLGetDiagRec**:  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1  
Diagnostic Msg:   "[Microsoft][ODBC Rdb Driver][Rdb] %SQL-F-RELNOTDEF, Table EMPLOYEE "  
                  "is not defined in schema."  
```  
  
 因為資料來源中發生錯誤，此驅動程式會加入診斷訊息 ([Rdb]) 的資料來源識別碼的前置詞。 由於驅動程式所使用的資料來源的元件，它會加入至診斷訊息的前置詞，其供應商 ([Microsoft]) 和識別項 （[ODBC Rdb 驅動程式]）。
