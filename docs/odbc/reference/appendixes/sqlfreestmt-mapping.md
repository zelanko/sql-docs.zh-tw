---
title: SQLFreeStmt 映射 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9d187db4d40132385b9ae4564fddbf89987e3e97
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302009"
---
# <a name="sqlfreestmt-mapping"></a>SQLFreeStmt 對應
當應用程式透過 ODBC *3.x*驅動程式呼叫**SQLFreeStmt** *選項參數SQL_DROP*時,呼叫  
  
```  
SQLFreeStmt(hstmt, SQL_DROP)   
```  
  
 對應  
  
```  
SQLFreeHandle(SQL_HANDLE_STMT,Handle)  
```  
  
 將*Handle*參數設置為*hstmt*中的值。
