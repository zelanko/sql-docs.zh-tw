---
title: 基於 DBMS 的驅動程式診斷範例 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304349"
---
# <a name="dbms-based-driver-diagnostic-example"></a>以 DBMS 為基礎的驅動程式診斷範例
基於 DBMS 的驅動程式向 DBMS 發送請求,並透過驅動程式管理員將資訊返回給應用程式。 由於驅動程式是與驅動程式管理器介面的元件,因此它格式化並返回**SQLGetDiagRec**的參數。  
  
 例如,如果使用 SQL/服務,Oracle Rdb 的 Microsoft 驅動程式遇到無效的游標名稱,它可能會從**SQLGetDiagRec**傳回以下值 :  
  
```  
SQLSTATE:         "34000"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Rdb Driver]Invalid cursor name: EMPLOYEE_CURSOR."  
```  
  
 由於錯誤發生在驅動程式中,因此它將首碼添加到供應商 ([Microsoft]) 和驅動程式 ([ODBC Rdb 驅動程式])的診斷消息中。  
  
 如果 DBMS 找不到表 EMPLOYEE,驅動程式可能會格式化並從**SQLGetDiagRec**傳回以下值 :  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1  
Diagnostic Msg:   "[Microsoft][ODBC Rdb Driver][Rdb] %SQL-F-RELNOTDEF, Table EMPLOYEE "  
                  "is not defined in schema."  
```  
  
 由於錯誤發生在數據源中,驅動程式向診斷消息添加了數據源標識符 ([Rdb]) 的首碼。 由於驅動程式是與數據源介面的元件,因此它將供應商 ([Microsoft]) 和識別碼 ([ODBC Rdb 驅動程式]) 的前置碼添加到診斷訊息中。
