---
title: SQLAllocStmt 映射 |微軟文件
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
ms.openlocfilehash: 447233a3ba014a5ef92f2f49840ad302f8aeccf0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305481"
---
# <a name="sqlallocstmt-mapping"></a>SQLAllocStmt 對應
當應用程式透過 ODBC *3.x*驅動程式呼叫**SQLAllocStmt**時,呼叫:  
  
```  
SQLAllocStmt(hdbc, phstmt)  
```  
  
 驅動程式中的驅動程式管理器映射到**SQLAllocHandle,** 如下所示:  
  
```  
SQLAllocHandle(SQL_HANDLE_STMT, InputHandle, OutputHandlePtr)  
```  
  
 與*輸入句柄*設定為*hdbc*與*輸出片控點的 Ptr*設定為*phstmt*。
