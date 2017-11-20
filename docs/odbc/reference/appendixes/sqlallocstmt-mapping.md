---
title: "SQLAllocStmt 對應 |Microsoft 文件"
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
- mapping deprecated functions [ODBC], SQLAllocStmt
- SQLAllocStmt function [ODBC], mapping
ms.assetid: a2449dbb-1b6c-4b49-81b9-ebdddd4442fd
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e8361f0b77e8f15f775eece7aae9b599be5e62ac
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlallocstmt-mapping"></a>SQLAllocStmt 對應
當應用程式呼叫**SQLAllocStmt**透過 ODBC 3*.x*驅動程式，會呼叫：  
  
```  
SQLAllocStmt(hdbc, phstmt)  
```  
  
 對應至**SQLAllocHandle**由驅動程式管理員在驅動程式中，如下所示：  
  
```  
SQLAllocHandle(SQL_HANDLE_STMT, InputHandle, OutputHandlePtr)  
```  
  
 與*InputHandle*設*hdbc*和*OutputHandlePtr*設*phstmt*。

