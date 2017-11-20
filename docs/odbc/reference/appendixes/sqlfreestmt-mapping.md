---
title: "SQLFreeStmt 對應 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLFreeStmt function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLFreeStmt
ms.assetid: 267d95f2-4f0c-47ab-9411-5afe105215a2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: df3cfba17f19074fbe00f33ef7fba098a4fe8184
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlfreestmt-mapping"></a>SQLFreeStmt 對應
當應用程式呼叫**SQLFreeStmt**與*選項*引數到 ODBC 3 SQL_DROP*.x*驅動程式，會呼叫  
  
```  
SQLFreeStmt(hstmt, SQL_DROP)   
```  
  
 對應到  
  
```  
SQLFreeHandle(SQL_HANDLE_STMT,Handle)  
```  
  
 與*處理*引數設定中的值為*hstmt*。

