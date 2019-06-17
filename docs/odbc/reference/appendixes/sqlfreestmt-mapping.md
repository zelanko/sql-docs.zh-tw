---
title: SQLFreeStmt Mapping | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFreeStmt function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLFreeStmt
ms.assetid: 267d95f2-4f0c-47ab-9411-5afe105215a2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1872806265470327f3e7bff468be2ba6d9011421
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199429"
---
# <a name="sqlfreestmt-mapping"></a>SQLFreeStmt 對應
當應用程式呼叫**SQLFreeStmt**具有*選項*引數到 ODBC 3 SQL_DROP *.x*驅動程式，會呼叫  
  
```  
SQLFreeStmt(hstmt, SQL_DROP)   
```  
  
 對應至  
  
```  
SQLFreeHandle(SQL_HANDLE_STMT,Handle)  
```  
  
 具有*處理*引數設定中的值為*hstmt*。
