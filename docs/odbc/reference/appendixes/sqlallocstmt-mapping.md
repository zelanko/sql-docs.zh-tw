---
description: SQLAllocStmt 對應
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e8307dce9e95c98ff92912517d5b574883d6298c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424920"
---
# <a name="sqlallocstmt-mapping"></a>SQLAllocStmt 對應
當應用程式*透過 ODBC 3.x 驅動程式呼叫* **SQLAllocStmt**時，呼叫：  
  
```  
SQLAllocStmt(hdbc, phstmt)  
```  
  
 驅動程式管理員會在驅動程式中對應至 **SQLAllocHandle** ，如下所示：  
  
```  
SQLAllocHandle(SQL_HANDLE_STMT, InputHandle, OutputHandlePtr)  
```  
  
 將 *InputHandle* 設定為 *hdbc* ，並將 *OutputHandlePtr* 設定為 *phstmt*。
