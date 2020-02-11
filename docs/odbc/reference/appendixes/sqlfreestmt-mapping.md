---
title: SQLFreeStmt 對應 |Microsoft Docs
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
ms.openlocfilehash: a92af35d8a1b1e98a484c69d7d2e66bf5bef3196
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68086083"
---
# <a name="sqlfreestmt-mapping"></a>SQLFreeStmt 對應
當應用程式以 SQL_DROP 的*Option*引數呼叫**SQLFreeStmt**時，透過*ODBC 3.x*驅動程式，呼叫  
  
```  
SQLFreeStmt(hstmt, SQL_DROP)   
```  
  
 對應至  
  
```  
SQLFreeHandle(SQL_HANDLE_STMT,Handle)  
```  
  
 將*Handle*引數設定為*hstmt*中的值。
