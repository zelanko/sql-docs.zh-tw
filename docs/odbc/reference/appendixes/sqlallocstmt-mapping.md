---
title: SQLAllocStmt 對應 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLAllocStmt
- SQLAllocStmt function [ODBC], mapping
ms.assetid: a2449dbb-1b6c-4b49-81b9-ebdddd4442fd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cf79d3ef813e87e785cea588cfc1d6e3eed44ee4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68064988"
---
# <a name="sqlallocstmt-mapping"></a>SQLAllocStmt 對應
當應用程式*透過 ODBC 3.x 驅動程式呼叫* **SQLAllocStmt**時，對的呼叫：  
  
```  
SQLAllocStmt(hdbc, phstmt)  
```  
  
 會由驅動程式中的驅動程式管理員對應至**SQLAllocHandle** ，如下所示：  
  
```  
SQLAllocHandle(SQL_HANDLE_STMT, InputHandle, OutputHandlePtr)  
```  
  
 將*InputHandle*設定為*hdbc* ，並將*OutputHandlePtr*設定為*phstmt*。
