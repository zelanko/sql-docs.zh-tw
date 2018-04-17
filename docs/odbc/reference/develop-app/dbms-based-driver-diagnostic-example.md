---
title: DBMS 架構驅動程式診斷的範例 |Microsoft 文件
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
ms.topic: article
helpviewer_keywords:
- DBMS-based driver diagnostic [ODBC]
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: a80d54b0-43ff-4dfd-b6cb-f4694a5ed765
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d67e352a67beca887a4283e7c89c5e97f993a0b9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="dbms-based-driver-diagnostic-example"></a>DBMS 架構驅動程式診斷的範例
DBMS 架構驅動程式將要求傳送至 DBMS，並傳回至應用程式透過驅動程式管理員的資訊。 驅動程式會是介面的驅動程式管理員元件，因為它已格式化，並傳回引數**SQLGetDiagRec**。  
  
 例如，如果 Oracle Rdb 時發生無效的資料指標名稱，請使用 SQL/服務，Microsoft 驅動程式，它可能會傳回下列值從**SQLGetDiagRec**:  
  
```  
SQLSTATE:         "34000"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Rdb Driver]Invalid cursor name: EMPLOYEE_CURSOR."  
```  
  
 驅動程式中發生錯誤，因為它加入前置詞診斷訊息 ([Microsoft]) 的廠商和驅動程式 （[ODBC Rdb 驅動程式]）。  
  
 如果 DBMS 找不到資料表員工，驅動程式可能會格式化，並傳回下列值從**SQLGetDiagRec**:  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1  
Diagnostic Msg:   "[Microsoft][ODBC Rdb Driver][Rdb] %SQL-F-RELNOTDEF, Table EMPLOYEE "  
                  "is not defined in schema."  
```  
  
 因為資料來源中發生錯誤，驅動程式新增到診斷訊息中的資料來源識別碼 ([Rdb]) 中的前置詞。 驅動程式因為 interfaced 與資料來源的元件，它會加入至診斷訊息的前置詞做為供應商 ([Microsoft])，並識別項 （[ODBC Rdb 驅動程式]）。
